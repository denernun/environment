```shell
#!/bin/bash

set -e

echo "Iniciando a instalação segura do RabbitMQ..."

# Define o codinome do Ubuntu
UBUNTU_CODENAME=$(lsb_release -cs)

echo "Codinome do Ubuntu: $UBUNTU_CODENAME"

# Verifica se o curl está instalado
if ! command -v curl &> /dev/null; then
    echo "Erro: curl não está instalado. Instalando..."
    sudo apt update
    sudo apt install -y curl
fi

# Remove repositórios antigos para evitar conflitos
echo "Removendo repositórios RabbitMQ/Erlang antigos..."
sudo rm -f /etc/apt/sources.list.d/rabbitmq.list
sudo rm -f /usr/share/keyrings/rabbitmq-*.gpg

# Instala dependências necessárias
echo "Instalando dependências..."
sudo apt update
sudo apt install -y gnupg apt-transport-https

# Importa a chave GPG do repositório Cloudsmith (Erlang)
echo "Importando chave GPG do Erlang..."
curl -fsSL https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-erlang.E495BB49CC4BBE5B.key \
  | sudo gpg --dearmor -o /usr/share/keyrings/rabbitmq-erlang.gpg

# Importa a chave GPG do repositório Cloudsmith (RabbitMQ)
echo "Importando chave GPG do RabbitMQ..."
curl -fsSL https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-server.9F4587F226208342.key \
  | sudo gpg --dearmor -o /usr/share/keyrings/rabbitmq-server.gpg

# Adiciona os repositórios Erlang e RabbitMQ
echo "Adicionando repositórios ao APT..."
cat <<SOURCES | sudo tee /etc/apt/sources.list.d/rabbitmq.list
## Erlang
deb [arch=amd64 signed-by=/usr/share/keyrings/rabbitmq-erlang.gpg] https://ppa1.rabbitmq.com/rabbitmq/rabbitmq-erlang/deb/ubuntu ${UBUNTU_CODENAME} main
## RabbitMQ
deb [arch=amd64 signed-by=/usr/share/keyrings/rabbitmq-server.gpg] https://ppa1.rabbitmq.com/rabbitmq/rabbitmq-server/deb/ubuntu ${UBUNTU_CODENAME} main
SOURCES

# Atualiza a lista de pacotes
echo "Atualizando a lista de pacotes..."
sudo apt update

# Instala Erlang e RabbitMQ
echo "Instalando Erlang e RabbitMQ..."
sudo apt install -y erlang-base \
    erlang-asn1 erlang-crypto erlang-eldap erlang-ftp erlang-inets \
    erlang-mnesia erlang-os-mon erlang-parsetools erlang-public-key \
    erlang-runtime-tools erlang-snmp erlang-ssl erlang-syntax-tools \
    erlang-tftp erlang-tools erlang-xmerl
sudo apt install -y rabbitmq-server

# Habilita e inicia o serviço
echo "Habilitando e iniciando o RabbitMQ..."
sudo systemctl enable rabbitmq-server
sudo systemctl start rabbitmq-server

# Aguarda o RabbitMQ iniciar
echo "Aguardando o RabbitMQ iniciar..."
sleep 10

# Remove o usuário guest padrão (inseguro)
echo "Removendo usuário guest padrão..."
sudo rabbitmqctl delete_user guest || true

# Gera uma senha forte para o administrador
ADMIN_PASSWORD=$(openssl rand -base64 16)
echo "Gerando senha forte para o usuário admin: $ADMIN_PASSWORD"

# Cria o usuário administrador
echo "Criando o usuário administrador..."
sudo rabbitmqctl add_user admin "${ADMIN_PASSWORD}"
sudo rabbitmqctl set_user_tags admin administrator
sudo rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"

# Habilita o plugin de gerenciamento web
echo "Habilitando o plugin de gerenciamento web..."
sudo rabbitmq-plugins enable rabbitmq_management

# Restarta para aplicar o plugin
echo "Restartando o RabbitMQ..."
sudo systemctl restart rabbitmq-server

echo ""
echo "RabbitMQ instalado e configurado com sucesso."
echo "Credenciais do administrador:"
echo "  Usuário: admin"
echo "  Senha: $ADMIN_PASSWORD"
echo "  Management UI: http://<ip-do-servidor>:15672"
echo "  AMQP: amqp://admin:${ADMIN_PASSWORD}@<ip-do-servidor>:5672"
echo "Lembre-se de configurar um FIREWALL para restringir o acesso às portas 5672 e 15672."

exit 0
```

## Redis
```bash
#!/bin/bash

set -e

echo "Iniciando a instalação segura do Redis..."

# Atualiza a lista de pacotes e atualiza o sistema
echo "Atualizando a lista de pacotes e atualizando o sistema..."
sudo apt update && sudo apt upgrade -y

# Instala o Redis Server sem interação
echo "Instalando o Redis Server..."
sudo apt install redis-server -y

# Verifica a versão do Redis
echo "Verificando a versão do Redis..."
redis_version=$(redis-cli -v | grep "v=" | awk -F '=' '{print $2}')
echo "Versão do Redis instalada: $redis_version"

# Inicia e habilita o serviço Redis
echo "Iniciando e habilitando o serviço Redis..."
sudo systemctl start redis-server
sudo systemctl enable redis-server

echo "Configurando a segurança do Redis..."

# Define uma senha forte para o usuário 'default' usando ACL
REDIS_PASSWORD=$(openssl rand -base64 32)
echo "Gerando uma senha forte para o Redis: $REDIS_PASSWORD"

# Modifica o arquivo de configuração para vincular ao localhost e manter protected-mode ativo
echo "Configurando bind para localhost e mantendo protected-mode ativo..."
sudo sed -i "s/^bind .*/bind 127.0.0.1 ::1/" /etc/redis/redis.conf
sudo sed -i "s/^protected-mode .*/protected-mode yes/" /etc/redis/redis.conf

# Adiciona a configuração ACL ao arquivo de configuração
echo "Adicionando configuração ACL ao arquivo redis.conf..."
sudo tee -a /etc/redis/redis.conf <<EOF

# Configuração ACL
user default on >$REDIS_PASSWORD allcommands allkeys

EOF

# Reinicia o serviço Redis para aplicar as configurações
echo "Reiniciando o serviço Redis para aplicar as configurações..."
sudo systemctl restart redis-server

echo "Segurança do Redis configurada com ACL."
echo "Para autenticar, use o comando 'AUTH default $REDIS_PASSWORD' no redis-cli."

exit 0
```

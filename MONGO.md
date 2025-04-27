## MONGO
**install**
```bash
#!/bin/bash

set -e

echo "Iniciando a instalação segura do MongoDB 6.0..."

# Define a versão do MongoDB
MONGODB_VERSION="6.0"

# Define o codinome do Ubuntu
UBUNTU_CODENAME=$(lsb_release -cs)

echo "Versão do MongoDB: $MONGODB_VERSION"
echo "Codinome do Ubuntu: $UBUNTU_CODENAME"

# Verifica se o curl está instalado
if ! command -v curl &> /dev/null; then
    echo "Erro: curl não está instalado. Instalando..."
    sudo apt update
    sudo apt install -y curl
fi

# Importa a chave GPG do MongoDB e salva diretamente em trusted.gpg.d
echo "Importando a chave GPG do MongoDB..."
curl -fsSL https://www.mongodb.org/static/pgp/server-${MONGODB_VERSION}.asc | sudo tee /etc/apt/trusted.gpg.d/mongodb-server-${MONGODB_VERSION}.gpg
chmod 644 /etc/apt/trusted.gpg.d/mongodb-server-${MONGODB_VERSION}.gpg

# Adiciona o repositório MongoDB à lista de fontes do APT
echo "Adicionando o repositório MongoDB à lista de fontes do APT..."
echo "deb [ arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/mongodb-server-${MONGODB_VERSION}.gpg ] https://repo.mongodb.org/apt/ubuntu ${UBUNTU_CODENAME}/mongodb-org/${MONGODB_VERSION} multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-${MONGODB_VERSION}.list

# Atualiza a lista de pacotes
echo "Atualizando a lista de pacotes..."
sudo apt update

# Instala o MongoDB sem interação
echo "Instalando o MongoDB..."
sudo apt install -y mongodb-org

# Habilita e inicia o serviço mongod
echo "Habilitando e iniciando o serviço mongod..."
sudo systemctl enable mongod
sudo systemctl start mongod
sudo systemctl status mongod

# Aguarda um pouco para o MongoDB iniciar
echo "Aguardando alguns segundos para o MongoDB iniciar..."
sleep 10

# Gera uma senha forte para o administrador
ADMIN_PASSWORD=$(openssl rand -base64 16)
echo "Gerando uma senha forte para o usuário admin: $ADMIN_PASSWORD"

# Cria o usuário administrador NO INÍCIO, ANTES de habilitar a autorização
echo "Criando o usuário administrador inicialmente..."
echo "
use admin
db.createUser({
  user: \"admin\",
  pwd: \"${ADMIN_PASSWORD}\",
  roles: [ { role: \"root\", db: \"admin\" } ]
})
" | mongosh --eval

# Configura o acesso remoto e habilita a autorização
echo "Configura o acesso remoto e habilita a autorização"
cat <<EOF | sudo tee /etc/mongod.conf
storage:
  dbPath: /var/lib/mongodb
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log
net:
  port: 27017
  bindIp: 0.0.0.0 # Alterado para permitir acesso de todas as interfaces
processManagement:
  timeZoneInfo: /usr/share/zoneinfo
security:
  authorization: enabled
EOF

# Restarta o serviço mongod para aplicar as configurações de segurança
echo "Restartando o serviço mongod para aplicar as configurações de segurança..."
sudo systemctl restart mongod

echo "MongoDB instalado, configurado para acesso remoto (em todas as interfaces) e autorização habilitada."
echo "Credenciais do administrador:"
echo "  Usuário: admin"
echo "  Senha: $ADMIN_PASSWORD"
echo "Lembre-se de configurar um FIREWALL para restringir o acesso à porta 27017 apenas das fontes desejadas."

exit 0
```
**uninstall**
```bash
#!/bin/bash

set -e

echo "Iniciando a remoção completa do MongoDB..."

# Define a versão do MongoDB (ajuste se necessário)
MONGODB_VERSION="6.0"

# Define o nome do arquivo da lista de fontes
MONGODB_LIST_FILE="/etc/apt/sources.list.d/mongodb-org-${MONGODB_VERSION}.list"

# 1. Para o serviço mongod
echo "Parando o serviço mongod..."
sudo systemctl stop mongod || true # Ignora erro se o serviço já estiver parado

# 2. Desativa o serviço para não iniciar na inicialização
echo "Desativando o serviço mongod..."
sudo systemctl disable mongod || true # Ignora erro se já estiver desativado

# 3. Remove os pacotes mongodb-org e suas dependências com purge
echo "Removendo os pacotes mongodb-org com purge..."
sudo apt remove --purge --auto-remove mongodb-org -y

# 4. Remove quaisquer outros pacotes relacionados ao mongodb-org (com curinga) com purge
echo "Removendo outros pacotes relacionados ao mongodb-org com purge..."
sudo apt-get purge mongodb-org* -y

# 5. Remove os diretórios de log e dados
echo "Removendo os diretórios de log e dados..."
sudo rm -rf /var/log/mongodb
sudo rm -rf /var/lib/mongodb

# 6. Remove o arquivo da lista de fontes do APT
echo "Removendo o arquivo da lista de fontes do APT..."
if [ -f "$MONGODB_LIST_FILE" ]; then
    sudo rm "$MONGODB_LIST_FILE"
else
    echo "Arquivo da lista de fontes '$MONGODB_LIST_FILE' não encontrado."
fi

# 7. Remove a chave GPG do MongoDB
echo "Removendo a chave GPG do MongoDB..."
sudo apt-key del --keyring /etc/apt/trusted.gpg.d/mongodb-server-${MONGODB_VERSION}.gpg "$(curl -fsSL https://www.mongodb.org/static/pgp/server-${MONGODB_VERSION}.asc | gpg --fingerprint | grep uid | awk '{print $5}')" || true

# 8. Atualiza a lista de pacotes
echo "Atualizando a lista de pacotes..."
sudo apt update

echo "Remoção completa do MongoDB concluída."

exit 0
```
**users**
```bash
mongosh -u "admin" -p "xxx" --authenticationDatabase admin

show dbs
use <database>
show users

# cria o usuario admin
db.createUser({user: "admin", pwd: "xxx", roles: [{ role: "root", db: "admin" }]})
db.updateUser("admin",{ pwd: "xxx" })
db.createUser({user: "admin", pwd: "xxx", roles: [{ role: "dbOwner", db: "<database>" }]})
```

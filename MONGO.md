## MONGO
**install**
```bash
#!/bin/bash

set -e

echo "Iniciando a instalação segura do MongoDB..."

# Define a versão do MongoDB
MONGODB_VERSION="7.0"

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

# Remove repositórios e chaves MongoDB antigos para evitar conflitos
echo "Removendo repositórios MongoDB antigos..."
sudo rm -f /etc/apt/sources.list.d/mongodb-org-*.list
sudo rm -f /usr/share/keyrings/mongodb-server-*.gpg

# Importa a chave GPG do MongoDB
echo "Importando a chave GPG do MongoDB..."
curl -fsSL https://www.mongodb.org/static/pgp/server-${MONGODB_VERSION}.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-${MONGODB_VERSION}.gpg --dearmor

# Adiciona o repositório MongoDB à lista de fontes do APT
echo "Adicionando o repositório MongoDB à lista de fontes do APT..."
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-${MONGODB_VERSION}.gpg ] https://repo.mongodb.org/apt/ubuntu ${UBUNTU_CODENAME}/mongodb-org/${MONGODB_VERSION} multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-${MONGODB_VERSION}.list

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
echo "mongosh -u \"admin\" -p \"$ADMIN_PASSWORD\" --authenticationDatabase admin"

exit 0
```
**uninstall**
```bash
#!/bin/bash

set -e

echo "*******************************************************"
echo "Desinstalação do MongoDB"
echo "*******************************************************"

# Para e desabilita o serviço
echo "Parando e desabilitando o serviço mongod..."
sudo systemctl stop mongod || true
sudo systemctl disable mongod || true

# Remove os pacotes do MongoDB
echo "Removendo pacotes do MongoDB..."
sudo apt purge -y mongodb-org mongodb-org-server mongodb-org-mongos \
    mongodb-org-shell mongodb-org-tools mongodb-org-database \
    mongodb-org-database-tools-extra mongodb-mongosh || true
sudo apt autoremove -y

# Remove repositórios e chaves GPG
echo "Removendo repositórios e chaves GPG..."
sudo rm -f /etc/apt/sources.list.d/mongodb-org-*.list
sudo rm -f /usr/share/keyrings/mongodb-server-*.gpg

# Remove dados e logs
echo "Removendo dados e logs do MongoDB..."
sudo rm -rf /var/lib/mongodb
sudo rm -rf /var/log/mongodb

# Remove arquivo de configuração
echo "Removendo arquivo de configuração..."
sudo rm -f /etc/mongod.conf

# Remove usuário e grupo do sistema
echo "Removendo usuário e grupo mongodb do sistema..."
sudo userdel -r mongodb 2>/dev/null || true
sudo groupdel mongodb 2>/dev/null || true

# Atualiza a lista de pacotes
echo "Atualizando a lista de pacotes..."
sudo apt update

echo ""
echo "MongoDB desinstalado com sucesso."

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

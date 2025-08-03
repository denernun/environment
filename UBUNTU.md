## environment
## install
```bash
#!/bin/bash

set -e

echo "*******************************************************"
echo "update"
echo "*******************************************************"

sudo apt update && sudo apt upgrade -y

echo "*******************************************************"
echo "certbot"
echo "*******************************************************"

sudo snap install --classic certbot
sudo snap set certbot trust-plugin-with-root=ok
sudo apt update && sudo apt install -y python3-certbot-dns-route53 -y



echo "*******************************************************"
echo "nginx"
echo "*******************************************************"

sudo apt install nginx -y

echo "Iniciando o serviço Nginx..."
sudo systemctl start nginx

echo "Verificando o status do Nginx..."
sudo systemctl status nginx

echo "Gerando arquivo dhparam.pem (isso pode levar alguns minutos)..."
sudo openssl dhparam -out /etc/nginx/dhparam.pem 4096

echo "Reiniciando o serviço Nginx..."
sudo systemctl reload nginx

LOGROTATE_FILE="/etc/logrotate.d/nginx"

sed -i \
    -e 's/daily/size 100M/g' \
    -e 's/rotate 14/rotate 0/g' \
    "$LOGROTATE_FILE"

if grep -q "size 100M" "$LOGROTATE_FILE" && grep -q "rotate 0" "$LOGROTATE_FILE"; then
    echo "Substituições aplicadas com sucesso!"
    echo "- 'daily' foi substituído por 'size 100M'"
    echo "- 'rotate 14' foi substituído por 'rotate 0'"
else
    echo "Aviso: Nem todas as substituições podem ter sido aplicadas."
    echo "Verifique o arquivo manualmente."
fi

echo "*******************************************************"
echo "nodejs"
echo "*******************************************************"

NODE_MAJOR=${1:-22} # Usa a versão 22 por padrão, mas permite especificar como argumento

echo "Instalando dependências e configurando o repositório NodeSource para Node.js ${NODE_MAJOR}.x..."

sudo apt update
sudo apt install -y ca-certificates curl gnupg
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_${NODE_MAJOR}.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
sudo apt update && sudo apt upgrade -y
sudo apt install nodejs -y
sudo apt install gcc g++ make -y

echo "Configurando variáveis de ambiente..."
echo "export NODE_ENV=production" | sudo tee -a ~/.bashrc
source ~/.bashrc # Aplica as alterações ao terminal atual

echo "Instalação concluída!"
echo "Node.js versão: $(node -v)"
echo "npm versão: $(npm -v)"

echo "*******************************************************"
echo "pm2"
echo "*******************************************************"

echo "Iniciando a instalação e configuração do PM2 e PM2 Logrotate..."

# Instala o PM2 globalmente sem interação
echo "Instalando PM2 globalmente..."
sudo npm install pm2@latest -g --yes
sudo pm2 startup systemd -u ubuntu --hp /home/ubuntu

# Instala o plugin PM2 Logrotate sem interação
echo "Instalando o plugin PM2 Logrotate..."
sudo pm2 install pm2-logrotate --silent

# Define a configuração do PM2 Logrotate sem interação
echo "Configurando o PM2 Logrotate..."
sudo pm2 set pm2-logrotate:max_size 10M
sudo pm2 set pm2-logrotate:compress false
sudo pm2 set pm2-logrotate:rotateInterval '* * * 1 0 0'

echo "PM2 e PM2 Logrotate instalados e configurados com sucesso!"
echo "Verifique a configuração com os comandos 'pm2 show pm2-logrotate' e 'pm2 logs'."

echo "*******************************************************"
echo "redis"
echo "*******************************************************"

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
**amplify**
```text
[nginx]
user = www-data
configfile = /etc/nginx/nginx.conf
stub_status = /stub_status
```
**wildcard**
```bash
$ create a user route53-user
$ add permission AmazonRoute53FullAccess
# create accesskey Application running on an AWS compute service

$ /root/.aws/credentials:
  [default]
  aws_access_key_id = SEU_ACCESS_KEY_ID
  aws_secret_access_key = SEU_SECRET_ACCESS_KEY

$ /root/.aws/config:
  [default]
  region = sa-east-1

#!/bin/bash
sudo certbot certonly --dns-route53 -d "*.domain.com.br" --email email@gmail.com
```
**renew**
```terminal
$ sudo nano /etc/letsencrypt/renew.sh
$ sudo chmod +x /etc/letsencrypt/renew.sh

#!/bin/bash
sudo service nginx stop
sudo certbot renew
sudo service nginx start
sudo systemctl reload nginx

$ crontab -e (todo 1 dia do mes as 3:00 da manha)
# 0 3 1 * * /etc/letsencrypt/renew.sh
```
**validation**
```terminal
$ https://www.ssllabs.com/ssltest/
```
**erros**
```bash
#!/bin/bash

set -e

echo "Limpando chaves obsoletas do apt..."

# Remove chave antiga da Ubuntu (se existir)
if [ -f /etc/apt/trusted.gpg.d/ubuntu-key-871920D1991BC93C.gpg ]; then
    sudo rm /etc/apt/trusted.gpg.d/ubuntu-key-871920D1991BC93C.gpg
    echo "Chave obsoleta da Ubuntu removida."
fi

# Remove chave antiga do PostgreSQL PGDG (se existir)
if [ -f /etc/apt/trusted.gpg.d/postgresql-key-7FCC7D46ACCC4CF8.gpg ]; then
    sudo rm /etc/apt/trusted.gpg.d/postgresql-key-7FCC7D46ACCC4CF8.gpg
    echo "Chave obsoleta do PostgreSQL PGDG removida."
fi

echo "Adicionando chaves usando o método atualizado (diretório trusted.gpg.d)..."

# Adiciona a chave da Ubuntu
wget -qO- "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x871920D1991BC93C&options=mr" | \
    sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/ubuntu-key-871920D1991BC93C.gpg
sudo chmod 644 /etc/apt/trusted.gpg.d/ubuntu-key-871920D1991BC93C.gpg
echo "Chave da Ubuntu adicionada ao trusted.gpg.d."

# Adiciona a chave do PostgreSQL PGDG
wget -qO- https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
    sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql-key-7FCC7D46ACCC4CF8.gpg
sudo chmod 644 /etc/apt/trusted.gpg.d/postgresql-key-7FCC7D46ACCC4CF8.gpg
echo "Chave do PostgreSQL PGDG adicionada ao trusted.gpg.d."

echo "Atualizando a lista de pacotes..."
sudo apt update

echo "Processo de limpeza e atualização das chaves concluído."

exit 0
```




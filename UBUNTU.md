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

echo "Adicionando script para renovacao do certificado"
sudo tee -a /etc/letsencrypt/renew.sh <<EOF
#!/bin/bash
sudo service nginx stop
sudo certbot renew
sudo service nginx start
sudo systemctl reload nginx
EOF
sudo chmod +x /etc/letsencrypt/renew.sh

echo "Adicionando script para rodar no crontab"
sudo tee -a /var/spool/cron/crontabs/ubuntu <<EOF
0 3 1 * * /etc/letsencrypt/renew.sh
EOF
sudo systemctl restart cron

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
sudo certbot certonly --dns-route53 -d "domain.com.br" -d "*.domain.com.br" --email email@gmail.com
```
**validation**
```terminal
$ https://www.ssllabs.com/ssltest/
```

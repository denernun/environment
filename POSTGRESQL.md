## Postgresql
**install**
```bash
#!/bin/bash

set -e

echo "Iniciando a instalação e configuração automatizada do PostgreSQL 16..."

# Adiciona a chave GPG do repositório PostgreSQL
echo "Adicionando a chave GPG do repositório PostgreSQL..."
curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg

# Adiciona o repositório PostgreSQL à lista de fontes do APT
echo "Adicionando o repositório PostgreSQL à lista de fontes do APT..."
echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list

# Atualiza a lista de pacotes e atualiza o sistema
echo "Atualizando a lista de pacotes e atualizando o sistema..."
sudo apt update && sudo apt upgrade -y

# Instala o PostgreSQL 16, contrib e client sem interação
echo "Instalando o PostgreSQL 16, contrib e client..."
sudo apt install postgresql-16 postgresql-contrib-16 postgresql-client-16 -y

# Configura o acesso remoto no postgresql.conf
echo "Configurando o acesso remoto no postgresql.conf..."
sudo sed -i "s/#listen_addresses = 'localhost'/listen_addresses = '*'/" /etc/postgresql/16/main/postgresql.conf

# Configura o acesso remoto no pg_hba.conf
echo "Configurando o acesso remoto no pg_hba.conf..."
sudo sed -i "\$ a host    all     all     0.0.0.0/0       scram-sha-256" /etc/postgresql/16/main/pg_hba.conf
sudo sed -i "\$ a host    all     all     ::0/0           scram-sha-256" /etc/postgresql/16/main/pg_hba.conf

# Inicia, para e reinicia o serviço PostgreSQL
echo "Iniciando o serviço PostgreSQL..."
sudo systemctl start postgresql

echo "Parando o serviço PostgreSQL..."
sudo systemctl stop postgresql

echo "Reiniciando o serviço PostgreSQL..."
sudo systemctl restart postgresql

echo "Instalação e configuração do PostgreSQL 16 concluídas com sucesso!"

exit 0
```
**uninstall**
```bash
#!/bin/bash

set -e

echo "Iniciando a remoção completa do PostgreSQL..."

# 1. Para o serviço PostgreSQL
echo "Parando o serviço PostgreSQL..."
sudo systemctl stop postgresql || true # Ignora erro se o serviço já estiver parado

# 2. Desativa o serviço para não iniciar na inicialização
echo "Desativando o serviço PostgreSQL..."
sudo systemctl disable postgresql || true # Ignora erro se já estiver desativado

# 3. Remove todos os pacotes relacionados ao PostgreSQL (incluindo configurações)
echo "Removendo todos os pacotes relacionados ao PostgreSQL..."
sudo apt-get --purge remove postgresql postgresql-* -y

# 4. Remove pacotes comuns e documentação (caso não tenham sido removidos)
echo "Removendo pacotes comuns e documentação..."
sudo apt-get --purge remove postgresql-common postgresql-doc -y

# 5. Remove dependências não utilizadas
echo "Removendo dependências não utilizadas..."
sudo apt autoremove -y

# 6. Remove diretórios de configuração (CUIDADO: PERDA DE CONFIGURAÇÕES)
echo "Removendo diretório de configuração (CUIDADO: PERDA DE CONFIGURAÇÕES)..."
sudo rm -rf /etc/postgresql

# 7. Remove diretório de dados (CUIDADO: PERDA DE TODOS OS BANCOS DE DADOS)
echo "Removendo diretório de dados (CUIDADO: PERDA DE TODOS OS BANCOS DE DADOS)..."
sudo rm -rf /var/lib/postgresql

echo "Remoção completa do PostgreSQL concluída."
echo "Execute 'dpkg -l | grep postgres' para verificar se ainda há pacotes instalados."

exit 0
```
**console**
```text
$ sudo su postgres
$ psql
$ alter user postgres with password '<password>';
# create database <db_name>;
```
**backup**
```text
$ pg_dump -h localhost -p 5432 -U postgres -d <dbname> -v -Fc -b -f /tmp/<dbname>.backup
# pg_restore -h localhost -p 5432 -U postgres -v -c -C -Fc -d <dbname> /tmp/<dbname>.backup
```

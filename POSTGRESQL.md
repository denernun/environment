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
sudo sed -i "\$ a local   all     all                     scram-sha-256" /etc/postgresql/16/main/pg_hba.conf
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
**/etc/postgresql/postgresql.conf**
```text
#------------------------------------------------------------------------------
# CUSTOMIZED OPTIONS
#------------------------------------------------------------------------------

# --- Connection Settings ---
listen_addresses                        = '*'

# --- Memória ---
shared_buffers                          = 2GB
work_mem                                = 32MB
maintenance_work_mem                    = 256MB
effective_cache_size                    = 6GB
wal_buffers                             = 64MB

# --- Conexões ---
max_connections                         = 100

# --- CPU ---
max_worker_processes                    = 4
max_parallel_workers                    = 4
max_parallel_workers_per_gather         = 2

# --- I/O (SSD) ---
random_page_cost                        = 1.1
effective_io_concurrency                = 200

# --- Checkpoint / WAL ---
checkpoint_completion_target            = 0.9
min_wal_size                            = 256MB
max_wal_size                            = 1GB
```
**/etc/pgbouncer/pgbouncer.ini**
```bash
[databases]
erpclass_admin = host=127.0.0.1 port=5432 dbname=erpclass_admin pool_size=15
erpclass_sync  = host=127.0.0.1 port=5432 dbname=erpclass_sync  pool_size=15
erpclass_whats = host=127.0.0.1 port=5432 dbname=erpclass_whats pool_size=5
erpclass_pix   = host=127.0.0.1 port=5432 dbname=erpclass_pix   pool_size=5
erpclass_hook  = host=127.0.0.1 port=5432 dbname=erpclass_hook  pool_size=5
mobiclass      = host=127.0.0.1 port=5432 dbname=mobiclass      pool_size=8
nfeclass       = host=127.0.0.1 port=5432 dbname=nfeclass       pool_size=8
erpclass_gps   = host=127.0.0.1 port=5432 dbname=erpclass_gps   pool_size=5

[pgbouncer]
listen_port = 6432
listen_addr = 127.0.0.1

auth_type  = scram-sha-256
auth_file  = /etc/pgbouncer/userlist.txt
auth_user  = pgbouncer_auth
auth_query = SELECT username, password FROM pgbouncer.get_auth($1)

pool_mode            = transaction
max_client_conn      = 400
default_pool_size    = 5
min_pool_size        = 1
reserve_pool_size    = 2
reserve_pool_timeout = 3

server_idle_timeout    = 30
client_idle_timeout    = 120
server_connect_timeout = 5
server_login_retry     = 5
query_timeout          = 60
client_login_timeout   = 10

ignore_startup_parameters = extra_float_digits, options, application_name

log_connections    = 0
log_disconnections = 0
log_pooler_errors  = 1
stats_period       = 60

admin_users = postgres
stats_users = postgres
```
**security**
```bash
$ psql

SELECT version();

CREATE ROLE pgbouncer_auth WITH LOGIN PASSWORD 'troque_por_senha_forte';

CREATE SCHEMA IF NOT EXISTS pgbouncer;

CREATE OR REPLACE FUNCTION pgbouncer.get_auth(p_usename TEXT)
RETURNS TABLE(username TEXT, password TEXT) AS $$
  SELECT usename::TEXT, passwd::TEXT
  FROM pg_catalog.pg_shadow
  WHERE usename = p_usename;
$$ LANGUAGE sql SECURITY DEFINER;

GRANT USAGE ON SCHEMA pgbouncer TO pgbouncer_auth;
GRANT EXECUTE ON FUNCTION pgbouncer.get_auth(text) TO pgbouncer_auth;

$ psql
# SET ROLE pgbouncer_auth;
# SELECT * FROM pgbouncer.get_auth('postgres');
# RESET ROLE;

sudo -u postgres psql -c "SELECT '\"' || rolname || '\" \"' || rolpassword || '\"' FROM pg_authid WHERE rolname = 'pgbouncer_auth';"
sudo -u postgres psql -c "SELECT '\"' || rolname || '\" \"' || rolpassword || '\"' FROM pg_authid WHERE rolname = 'postgres';"

colar em /etc/pgbouncer/userlist.txt

sudo mkdir -p /etc/systemd/system/pgbouncer.service.d
sudo nano /etc/systemd/system/pgbouncer.service.d/override.conf

[Service]
LimitNOFILE=65536

sudo systemctl daemon-reload
sudo systemctl restart pgbouncer
sudo systemctl status pgbouncer
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

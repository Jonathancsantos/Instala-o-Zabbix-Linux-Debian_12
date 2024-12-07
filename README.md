# Instalação Completa do Zabbix no Debian 12

## 1. Adicionar o Repositório do Zabbix:
### Execute os seguintes comandos para adicionar o repositório do Zabbix no Debian 12:
`wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_latest+debian12_all.deb
dpkg -i zabbix-release_latest+debian12_all.deb
apt update`

## 2. Instalar o Zabbix Server, Frontend e Agent:
### Instale os pacotes necessários para o Zabbix Server, Frontend e Agent:
`apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent`

## 3. Configurar o Banco de Dados MariaDB:
### Instale o MariaDB e configure o banco de dados para o Zabbix:
`apt install mariadb-server`
### No prompt do MySQL, insira a senha do usuário root e execute os seguintes comandos para configurar o banco de dados:
`mysql -uroot -p
password
mysql> create database zabbix character set utf8mb4 collate utf8mb4_bin
mysql> create user zabbix@localhost identified by 'password'
mysql> grant all privileges on zabbix.* to zabbix@localhost
mysql> set global log_bin_trust_function_creators = 1
mysql> quit`

## 4. Importar o Esquema do Banco de Dados:
`zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix`

## 5. Configurar o Zabbix Server:
### Edite o arquivo de configuração do Zabbix Server para incluir a senha do banco de dados:
`nano /etc/zabbix/zabbix_server.conf`
### No arquivo de configuração, encontre a linha DBPassword e insira a senha configurada no passo anterior:
`DBPassword=password`
## 6. Reiniciar os Serviços:
### Reinicie e habilite os serviços do Zabbix:
`systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2`

## 7. Acessar o Zabbix Frontend:
### Para acessar o Zabbix Frontend, abra um navegador e use o endereço IP definido para o servidor seguido de /zabbix, como no exemplo:
`http:////192.168.0.100/zabbix`

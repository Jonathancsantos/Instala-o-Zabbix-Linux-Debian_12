# Comandos para a correta instalação do Zabbix no sistema operacional Debian_12

# 1.	Adicionar o Repositório do Zabbix:
wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_latest+debian12_all.deb
dpkg -i zabbix-release_latest+debian12_all.deb
apt update

# 2.	 Instalar o Zabbix Server, Frontend e Agent:
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent

# 3. Configurar o Banco de Dados MariaDB:
apt install mariadb-server,
mysql -uroot -p,
password,
mysql> create database zabbix character set utf8mb4 collate utf8mb4_bin,
mysql> create user zabbix@localhost identified by 'password',
mysql> grant all privileges on zabbix.* to zabbix@localhost,
mysql> set global log_bin_trust_function_creators = 1,
mysql> quit;

# 4.	 Importar o Esquema do Banco de Dados:
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix

# 5.	Configurar o Zabbix Server:
nano /etc/zabbix/zabbix_server.conf
DBPassword=password
# 6.	Reiniciar os Serviços:
   	systemctl restart zabbix-server zabbix-agent apache2
   	systemctl enable zabbix-server zabbix-agent apache2
8.	Acessar o Zabbix Frontend:
   	Acessar o frontend do Zabbix via navegador usando o endereço IP definido para o servidor /zabbix (//192.168.0.100/zabbix)

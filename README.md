# Instalação do Zabbix 7.0 LTS (Long Term Support) no Debian 12

Para esta pesquisa, optou-se pela versão do Zabbix 7.0 LTS. Abaixo estão os passos detalhados para realizar a instalação no Debian 12.

## 1. Adicionar o Repositório do Zabbix

Primeiro, adicione o repositório do Zabbix 7.0 LTS para Debian 12:

```bash
wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_latest+debian12_all.deb
dpkg -i zabbix-release_latest+debian12_all.deb
apt update


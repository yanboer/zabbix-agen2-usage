# deploy zabbix

## 1、deploy zabbix on VM

> os: Ubuntu Server 20.04.4 LTS 64bit


### a. install postgresql(Must be at least 13.0.)

##### (1) install postgresql
```bash
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get -y install postgresql-14
```

##### (2) alter param

1. edit `/etc/postgresql/14/main/postgresql.conf` file, alter `listen_addresses` param
```bash
listen_addresses = '*'
```

2. edit `/etc/postgresql/14/main/pg_hba.conf` file,
```bash
host all all 0.0.0.0/0 md5
```

3. restart postgresql
```bash
service postgresql restart
```

### b. deploy zabbix_server, zabbix_agent2, apache2

##### (1) install
```bash
wget https://repo.zabbix.com/zabbix/6.2/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.2-2%2Bubuntu20.04_all.deb
dpkg -i zabbix-release_6.2-2+ubuntu20.04_all.deb
apt update

apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent2 zabbix-agent2-plugin-*
```

> more zabbix repo please visit: https://www.zabbix.com/download

##### (2) postgresql database import zabbix initial schema and data
```bash
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
```

##### (3) edit `/etc/zabbix/zabbix_server.conf` file, add database password
```bash
DBPassword=password
```

##### (4) restart service
```bash
systemctl restart zabbix-server zabbix-agent2 apache2
```

## 2、deploy zabbix on container


### a. get source code
```bash
git clone https://github.com/yanboer/zabbix-agen2-usage.git
```

### b. start container
```bash
cd zabbix-agen2-usage
docker-compose up
```

> note: need docker and docker-compose env



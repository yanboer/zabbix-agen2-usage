# create.sql
`create.sql` file from zabbix-server-pgsql container, /usr/share/doc/zabbix-server-pgsql/create.sql.gz file

# zabbix dashboard
ip:8080 

user: Admin/zabbix

# usage

1. login web page
2. add host


xxx. add test data
```bash
pgbench -i -s 100 -U postgres test
pgbench -P 1 -c 32 -j 4 -T 300 -U postgres test
```
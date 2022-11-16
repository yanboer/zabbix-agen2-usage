# deploy zabbix
[deploy zabbix](deploy_zabbix.md)

# zabbix dashboard
ip:8080 or ip:80/zabbix

user: Admin(admin)/zabbix

# zabbix usage

1. login web page
2. add host(Configuration/Hosts)
![STEP1](_images/step0.png)

- a. set Host
![STEP1](_images/step1.png)

> MySQL template: MySQL by Zabbix agent 2
> 
> PostgreSQL template: PostgreSQL by Zabbix agent 2

![STEP1](_images/template.png)

- b. set Macros var

MySQL set：{$MYSQL.DSN} {$MYSQL.PASSWORD} {$MYSQL.USER}
PostgreSQL set: {$PG.DATABASE} {$PG.PASSWORD} {$PG.URI} {$PG.USER}

![STEP1](_images/step2.png)

3. test data(Monitoring/Latest data)
![STEP1](_images/step3.png)



xxx. add test data
```bash
pgbench -i -s 100 -U postgres test
pgbench -P 1 -c 32 -j 4 -T 300 -U postgres test
```


# others

### 1、 create.sql
`create.sql` file from zabbix-server-pgsql container, /usr/share/doc/zabbix-server-pgsql/create.sql.gz file

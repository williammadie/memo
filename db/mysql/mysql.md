# MySQL

## Service

Start service
```bash
sudo /etc/init.d/mysql start
```

Stop service
```bash
sudo /etc/init.d/mysql stop
```

Restart service
```bash
sudo /etc/init.d/mysql start
```

## Connection
First connection :

```bash
sudo mysql -u root
```

Normal connection :

```bash
mysql -p
```

## Most used

### Navigation
> List all databases
```sql
SHOW DATABASES;
```
> Select a database
```sql
USE dbname;
```
> List all tables inside a database
```sql
SHOW TABLES;
```

> See columns information of a table
```sql
DESCRIBE tablename;
```

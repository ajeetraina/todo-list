## Using Compose

```
 docker compose up -d --build
```

```
docker compose ps
NAME                    IMAGE            COMMAND                  SERVICE   CREATED              STATUS              PORTS
using-compose-app-1     node:21-alpine   "docker-entrypoint.s…"   app       About a minute ago   Up About a minute   0.0.0.0:3000->3000/tcp
using-compose-mysql-1   mysql:8.0        "docker-entrypoint.s…"   mysql     About a minute ago   Up About a minute   3306/tcp, 33060/tcp
```

## How to test it?

Open Docker Dashboard > MySQL container > Exec


```
sh-4.4# mysql -u root -p
Enter password: secret
```

```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 12
Server version: 8.0.36 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| todos              |
+--------------------+
5 rows in set (0.01 sec)
```

```
mysql> use todos;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
```

```
mysql> show tables;
+-----------------+
| Tables_in_todos |
+-----------------+
| todo_items      |
+-----------------+
1 row in set (0.00 sec)
```

Let's add "watch netflix" to the todo-list item:

```
mysql> select * from todo_items;
+--------------------------------------+---------------+-----------+
| id                                   | name          | completed |
+--------------------------------------+---------------+-----------+
| 852710b0-0c6d-4e8e-99a6-e61007022cd3 | Watch netflix |         0 |
+--------------------------------------+---------------+-----------+
1 row in set (0.00 sec)
```
 

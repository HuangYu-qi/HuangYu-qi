### RBAC设计模式心得

"RBAC"数据库设计模式，是基于角色权限控制，也就是说是“**用户—角色—权限**”模式，避免了“ACL”的“用户—权限”模式管理松散，无法集中管理的问题。

“RBAC”的优点:*简化了用户和权限的关系，易于扩展和维护,易于整理，避免了一个用户多种角色和权限之间管理的复杂性，权限管理非常方便*。用户是通过角色来拥有权限的，也就是用户跟角色有关联，而跟权限没有关联；我们可以通过管理组来与用户关联，这样的话我们需要给组赋权限，让组与用户关联。

进行数据库设计主要需要创建五个表，**用户表、权限表、角色表、角色表和权限表、用户和角色表**，然后在创建两个链接表（**链接菜单表、用户和链接菜单表**）用于连接权限。

每个用户至少具备一个权限，每个用户至少扮演一个角色；可以对两个完全不同的角色分配完全相同的访问权限；会话由用户控制，一个用户可以创建会话并激活多个用户角色，从而获取响应的访问权限，用户可以在会话中更改激活角色，并且用户可以主动结束一个会话；用户和角色是多对多的关系，表示一个用户在不同的场景下可以拥有不同的角色。

### 创建表

mysql> create database the_first;

Query OK, 1 row affected (0.00 sec)

mysql> show databases;

+--------------------+

| Database           |

+--------------------+

| information_schema |

| the_first             |

| mysql              |

| one                |

| performance_schema |

| sakila             |

| test               |

| world              |

+--------------------+

8 rows in set (0.00 sec)

mysql> use the_first;

Database changed

mysql> create table users(

    -> id int comment 'id',
    
    -> name varchar(32) comment 'name',
    
    -> status varchar(32) comment 'status'
    
    -> );
    
Query OK, 0 rows affected (0.22 sec)

mysql> insert into user values(1,'张三,'销售');

Query OK, 1 row affected (0.05 sec)

mysql> insert into user values(2,'李四','前台');

Query OK, 1 row affected (0.04 sec)

mysql> update user set id=3;

Query OK, 2 rows affected (0.07 sec)

Rows matched: 2  Changed: 2  Warnings: 0

mysql> delete from user where name='王五';
Query OK, 1 row affected (0.03 sec)

mysql> select*from user;
+------+------+--------+
| id   | name | status |
+------+------+--------+
|    3 | 李四  | 前台 |
+------+------+--------+
1 row in set (0.00 sec)

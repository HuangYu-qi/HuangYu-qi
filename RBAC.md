### RBAC设计模式心得

"RBAC"数据库设计模式，是基于角色权限控制，也就是说是“**用户—角色—权限**”模式，避免了“ACL”的“用户—权限”模式管理松散，无法集中管理的问题。

“RBAC”的优点:*简化了用户和权限的关系，易于扩展和维护,易于整理，避免了一个用户多种角色和权限之间管理的复杂性，权限管理非常方便*。用户是通过角色来拥有权限的，也就是用户跟角色有关联，而跟权限没有关联；我们可以通过管理组来与用户关联，这样的话我们需要给组赋权限，让组与用户关联。

进行数据库设计主要需要创建五个表，**用户表、权限表、角色表、角色表和权限表、用户和角色表**，然后在创建两个链接表（**链接菜单表、用户和链接菜单表**）用于连接权限。

每个用户至少具备一个权限，每个用户至少扮演一个角色；可以对两个完全不同的角色分配完全相同的访问权限；会话由用户控制，一个用户可以创建会话并激活多个用户角色，从而获取响应的访问权限，用户可以在会话中更改激活角色，并且用户可以主动结束一个会话；用户和角色是多对多的关系，表示一个用户在不同的场景下可以拥有不同的角色。

### 创建表

create database the_first;

use the_first;

###### 创建用户表users
create table users(

id int comment '编号',

name VARCHAR(32) comment '姓名',

occupation VARCHAR(255) comment '职业'

);

###### 创建角色表
create table roles(

occ1 VARCHAR(32) comment '销售',

occ2 VARCHAR(32) comment '经理',

occ3 VARCHAR(32) comment '前台'

);

###### 创建权限表
create table access(

acc1 VARCHAR(255) comment '添加顾客',

acc2 VARCHAR(255) comment '删除顾客',

acc3 VARCHAR(255) comment '查看顾客名单'

);

###### 创建角色和权限表
create table roleaccess(

ra1 VARCHAR(255) comment '销售可以添加顾客',

ra2 VARCHAR(255) comment '经理可以删除顾客',

ra3 VARCHAR(255) comment '前台可以查看顾客名单'

);

###### 给users表中添加数据



###### 创建用户和角色表
create table userrole(

ur1 VARCHAR(255) comment '张三是销售',

ur2 VARCHAR(255) comment '李四是经理',

ur3 VARCHAR(255) comment '王五是前台'

);

```
createtime: 2025-11-19
```

# 问题详情

```
Driver class ‘com.intellij.execution.rmi.RemoteServer‘ not found.
```

数据库driver的版本太高了，数据库要选择低版本的

```
ORA-32795: 无法插入到“始终生成”身份列
```

id列插入时要写，不会自动生成

```
[42000][1950] ORA-01950: 对表空间 'USERS' 无权限
```

授权

```
SQL> grant resource to oracle;  # 给oracle这个账户授予resource的角色，拥有这个角色后oracle就可以创建数据库对象，解决了能创建表的问题

授权成功。

SQL> alter user oracle quota unlimited on users;  
# 给用户oracle在USERS表空间设置无限配额，新创建的用户默认是没有表空间配额的，quota unlimited on users表示这个用户在USERS表空间上可以无限使用空间
# 解决了创建表以后可以存储数据的问题

用户已更改。
```



# 解决过程

从`cmd`进入控制台的方法

```
sqlplus/nolog

sqlplus / as sysdba
```

# 思考

为什么是给users表空间授权就可以存数据了呢？

因为Oracle数据库中所有的数据都是放在表空间里面的，只有先给表空间授权才能存放数据
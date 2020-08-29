## 基本

### 安装

```shell
sudo apt install mysql-server
sudo apt install mysql-client
```

### 配置

```
# 查询密码
cat /etc/mysql/debian.conf

# 设置密码
mysql> update user set authentication_string=password('password') where user='root';
mysql> update user set plugin="mysql_native_password"; 
# 允许 root 远程登录
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
# 刷新
mysql> flush privileges;
mysql> quit;
```

### 绑定端口

```
sudo cat /et/mysql/my.cnf

...
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mysql.conf.d/

sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf

bind-address        = 0.0.0.0

sudo systemctl restart mysql.service

```



## 彻底卸载 apt 安装的mysql

```
# 查看 mysql 依赖
dpkg --list|grep mysql
# 先卸载 mysql-common
sudo apt-get remove mysql-common
sudo apt-get autoremove --purge mysql-server-5.0 
# 查看还有什么依赖
dpkg --list|grep mysql
# 清楚残留数据
dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
```


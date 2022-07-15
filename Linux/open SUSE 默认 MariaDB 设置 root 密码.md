open SUSE 安装之后，默认安装了 MariaDB 数据库。使用下面步骤，可以设置 root 密码

>启动服务
```shell
sudo systemctl restart mysql
```

>开机自启（根据需要使用）
```shell
sudo systemctl enable mysql
```

>修改 root 密码为 123456
```shell
sudo mysqladmin -u root password "123456"
```

>登录数据库
```shell
mysql -u root -p
```

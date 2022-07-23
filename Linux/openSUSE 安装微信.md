此方法虽然是的 openSUSE 上测试的，但所有Linux 都可通用。

在优麒麟官网下载最新的 deb 打包的微信 https://www.ubuntukylin.com/applications/106-cn.html

右键解压deb 文件，进入解压后的文件，再解压 control.tar.xz 和 data.tar.xz 文件，此时会得到 control 文件夹和 data 文件夹。

将解压后的 data.tar.xz 里面的所有文件，复制到根目录。

```shell
cd data
sudo cp -R * /
```

找到 control 文件夹中的 postinst 文件，将此文件设置为可执行文件，然后执行此文件。

这个文件中最后有两个 mv 命令，第一个会出错不用官，第二个可以正常执行，需要单独执行一下。

>postinst
```shell
#!/bin/bash

# Link to the binary
ln -sf '/opt/weixin/weixin' '/usr/bin/weixin'

# SUID chrome-sandbox for Electron 5+
chmod 4755 '/opt/weixin/chrome-sandbox' || true

update-mime-database /usr/share/mime || true
update-desktop-database /usr/share/applications || true

mv /etc/lsb-release /etc/lsb-release-test
mv /etc/lsb-release-ukui /etc/lsb-release

```

postrm 是卸载文件，执行方式和上面一样。不过貌似卸载的不是很干净。

>postrm
```shell
#!/bin/bash

# Delete the link to the binary
rm -f '/usr/bin/weixin'
mv /etc/lsb-release-test  /etc/lsb-release
```

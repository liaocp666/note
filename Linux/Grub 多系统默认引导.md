自动进入上一次引导的系统配置

编辑  `/etc/default/grub` 文件

```shell
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=true
```

保存后，执行更新 grub 命令

```shell
sudo update-grub
```
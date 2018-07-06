## linux 命令

```shell
sudo su // 切换到root账户
sudo -su me // 切换到me账户
```

当在linux下创建用户时，会在`home/username`目录下 创建用户目录，在用户目录下，该用户拥有全部的权限

使用putty 和 winSCP 使用拖拽的方式连接linux，使用ssh不能使用root账号登陆

```shell
ls -l
drwx---rw- root root
目录 读写执行（可以进入） 列出用户的权限 --拥有者 用户组 其他
```
## 常用的linux 命令

> http://blog.csdn.net/xufei512/article/details/53321980

### 1、创建目录
```shell
mkdir 
```

### 2、删除目录
```shell
rm -fr dir // remove focus recursive 强制递归删除文件夹下的所有内容
```
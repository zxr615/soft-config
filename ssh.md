## SSH

## 生成 ssh-key

`ssh-keygen -t rsa -C "12345@qq.com"`



## 免密远程 SSH 登录

将本地 `id_rsa.pub` 添加到服务端 `authorized_keys`中

```
# 客户端
`cat ~/.ssh/id_rsa.pub`

# 服务端将客户端的「id_rsa.pub」追加进 「authorized_keys」中
sudo vim ~/.ssh/authorized_keys

# 免密登录
SSH fanwei@192.168.0.1
```



## 区分多个服务器

客户端：

```
vim ~/.ssh/config

Host ubuntu
    HostName fanwei.cn
    Port 22
    User fanwei
    IdentityFile ~/.ssh/id_rsa
    
Host ubuntu2
    HostName fanwei2.cn
    Port 22
    User fanwei
    IdentityFile ~/.ssh/id_rsa
```

免密登录：`SSH ubuntu`



## PhpStorm Terminal 中配置快捷登录 ssh

`Settings -> Tools -> Terminal`

![image-20200830204459428](https://cdn.jsdelivr.net/gh/zxr615/md-images/images/2020/image-20200830204459428.png)


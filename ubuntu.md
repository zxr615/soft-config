## ubuntu

## 基本设置

- 安装 net-tools
  ```shell
  # 可使用 ifconfig 命令
  sudo apt install net-tools
  ```

- 允许 root 登录

  ```shell
  vim /etc/ssh/sshd_config
  
  PermitRootLogin yes
  
  reboot
  ```

- gnu nano 替换成 vim

  ```
  sudo update-alternatives --config editor 
  # 选择 vim.basic
  ```

- sudo 免密码[^1]

  ```
  sudo visudo
  # 密码超时设置
  Defaults env_reset, timestamp_timeout=x
  x = 分钟，0 = 每次都要输入密码， -1 = 记住密码
  
  # 免 sudo 密码设置
  # fanwei 用户执行 vim 命令时不需要输入密码
  fanwei ALL=(ALL) NOPASSWD: vim
  
  # fanwei 用户执行任何命令都不需要输入密码
  fanwei ALL=(ALL) NOPASSWD: ALL
  ```

- 关闭防火墙

  ```
  # 状态
  systemctl status ufw
  # 关闭
  systemctl stop ufw
  # 禁止开机自启
  systemctl disable ufw
  ```




## 常用软件

- 上传工具 lrzsz

    ```
    sudo apt install lrzsz
    
    # 远程工具设置文件传输为：ZModem
    命令：rz
    ```




## Ref

[^1]:不输入密码执行sudo命令

<img src="https://raw.githubusercontent.com/zxr615/md-images/master/images20210107230551.png" alt="image-20210107230551027" style="zoom: 20%; float:left"/>
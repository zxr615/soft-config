## ubuntu

## 基本设置

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

- sudo 记住密码时间

  ```
  sudo visudo
  Defaults env_reset, timestamp_timeout=x
  x = 分钟，0 = 每次都要输入密码， -1 = 记住密码
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

    
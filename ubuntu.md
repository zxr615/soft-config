## ubuntu

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

  
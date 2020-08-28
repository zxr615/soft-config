## proxychains

- 安装

```shell
sudo apt isntall tor
sudo apt install proxychains
```

- 配置

  ` /etc/proxychains.conf `

- 内容

  ```shell
  # proxy_dns
  socks5 主机ip 1080
  ```

- 测试

  `proxychains curl baidu.com`

- alias

  `alias pcs=proxychains`

- 其他

  ssr端需要开启 ‘允许本地代理:来自局域网连接’

  clash需要开启‘局域网代理’

  参考文章：https://blog.popkx.com/Ubuntu-install-proxychains-let-terminal-using-socks5-proxy-speed-up-downloading/
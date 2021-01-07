# WSL2

## ssh 开机自启

- 查看 wsl name
    ```shell
    PS C:\Users\fanwei> wsl -l -v
      NAME      STATE           VERSION
    * Ubuntu    Running         2
    ```

- 新建自启 bat 文件

    ```shell
    vim startupWslSSH.bat
    # 写入
wsl.exe -d Ubuntu sudo service ssh start
    ```

- 将文件新增到开机自启

    ```
    win + r -> shell:startup
    ```

    
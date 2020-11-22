# xshell



## 复制、粘贴、终止目前的命令配置

> 由于在 xshell 中，或者说是在 Windows 命令行中，复制快捷 `ctrl + c` 键被 `终止目前命令` 占用，使用起来实在不方便，每当想复制内容时都变成了 `终止目前命令`，所以按照平时自己使用的习惯修改了一下 `xshell` 配置。

### 1：更改 `ctrl + c`、`ctrl + v` 为复制粘贴，图中展示了复制，粘贴同理

![xshell-ctrl-c](https://cdn.jsdelivr.net/gh/zxr615/md-images/images/2020/xshell-ctrl-c.png)

![](https://cdn.jsdelivr.net/gh/zxr615/md-images/images/2020/image-20201122151141693.png)



> 由于把 `ctrl + c` 修改成了 `复制` 功能，就无法执行 `中断目前命令`  功能了，这时候可以修改一下 linux 系统中的 `stty` 改变一下 `中断目前命令` 快捷键



### 2：修改 `中断目前命令` 快捷键

> stty (setting tty 终端机的意思) 

```shell
stty -a
```

红色框中就是 `中断目前命令` 的快捷键，默认的就是 `ctrl + c` 

![image-20201122152926408](https://cdn.jsdelivr.net/gh/zxr615/md-images/images/2020/image-20201122152926408.png)

这里我不准备直接修改 `intr` 的值，可以通过个人自定义环境变量设置快捷键

改成 `ctrl + b` 为 `中断目前命令` 快捷键

```shell
# 追加到配置文件中
echo "stty intr "^b"" >> ~/.zshrc
# 使配置文件生效
source ~/.zshrc
```

注：我这是使用 zsh 所以是写入到了 `~/.zshrc` 文件中，如果是使用 `bash` 的话要写入到  `~/.bash_profile` 中。



### 3：测试，已经变成 `ctrl + b` 

![image-20201122154915882](https://cdn.jsdelivr.net/gh/zxr615/md-images/images/2020/image-20201122154915882.png)



## 总结

改成`ctrl + b` 的原因是因为这个快捷键似乎没有什么冲突，加上就在 `ctrl + ` 的旁边，比较方便，当然你想改成其他的也没问题，但只能是 `ctrl + *`，因为 `ctrl + *` 是 `ASCII` 控制字符[^ 1][^2]

也可以直接对 `intr` 快捷键直接修改，但不建议这么做，具体原因请参考下面鸟哥的文章



参考文章：

[**鸟哥 - 终端机的环境配置： stty,  set**](http://cn.linux.vbird.org/linux_basic/0320bash.php#settings_set)

[^1]: http://www.physics.udel.edu/~watson/scen103/ascii.htm
[^2]: https://zh.wikipedia.org/wiki/%E6%8E%A7%E5%88%B6%E5%AD%97%E7%AC%A6
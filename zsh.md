# zsh

## 安装

- zsh

    `apt install zsh`

- 安装oh-my-zsh

  `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

- 使用 zsh 替换 bash

  `chsh -s 'which zsh' #重启生效`

- 安装插件

  - autojump
    - `apt install autojump`
  - zsh-autosuggestion
    - `git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions`
  - zsh-syntax-highlighting
    - `git clone git://github.com/zsh-users/zsh-syntax-highlighting $ZSH_CUSTOM/plugins/zsh-syntax-highlighting`

- 开启插件

  ```shell
  vim ~/.zshrc
  # 在文件里找到plugins，添加
  plugins=(
    git
    autojump
    zsh-autosuggestions
    # 命令是否正确提示，放在最下面
    zsh-syntax-highlighting
  )
  ```




## root 用户

> 将当前用户的 zsh 配置文件软链到 root 家目录中，这样两个用户可以使用同一个 zsh 配置

```
sudo ln -s $HOME/.oh-my-zsh /root/.oh-my-zsh
sudo ln -s $HOME/.zshrc /root/.zshrc

# 替换 zsh
root > chsh -s 'which zsh'
```


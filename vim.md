## vim

`vim ~/vimrc`

```shell
 set nu “ 显示行
 set ts=4 ” tab 为 4 个空格
 syntax = on “ 语法提示
 set autoindent ” 自et ts=4缩进
 " 改变 d 剪切 为 删除
 nnoremap d "_d
 vnoremap d "_d
 
 " 避免忘记 sudo 不能保存问题
 cmap w!! w !sudo tee > /dev/null %
```


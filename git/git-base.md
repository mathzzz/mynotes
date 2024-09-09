
# 初始化git仓库
```
git init
```

# 查看git用户，邮箱，编辑器
```
git config --list
git config --show-origin --list

```

# 配置git用户，邮箱，编辑器
```
git config user.name zxm
git config user.email zhuangxm@163.com
git config --global core.editor vim
```

# 查看当前所在分支
``` shell
git branch -a
```

# 创建本地分支
``` shell
git branch dev
```

# 切换到特定分支
```
git checkout dev
```


# 修改并提交到本地分支

## 编辑文件
``` shell 
echo >readme.md
```

##  添加注释提交到暂存区
``` shell
git add readme.md
git commit -m "first file"
```

## 提交本地修改到远程分支
``` shell
git push -u origin
```

# 理解git push的默认行为
+ 在没有指定任何参数的情况下，git push 命令会默认将当前分支推送到与之对应的远程分支。
  这个“对应”关系通常是在你第一次推送分支时使用 -u 参数建立的

``` shell
% git branch -vv
* dev  e2c6619 [origin/dev: ahead 1] mdf readme.md 2
  main 0aac3a0 [origin/main] Initial commit
```

+ 推送当前分支到远程的同名分支
``` git push```

+ 推送当前分支到远程的特定分支
``` git push origin feature-x:main ```




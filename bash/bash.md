# bash

## 查看中文bash
``` man -L zh_CN bash```
##  history 相关的变量
``` shell
HISTFILE # 默认为= ~/.bash_history 
HISTTIMEFORMAT='[+%F %T]'
HISTCONTROL=""
HISTIGNORE=""
HISTFILESIZE=50000 # 历史
HISTSIZE=1000 # 当前会话显示条目，默认为500
```

## 3n+1猜想
```shell
f3n1() { local -i n=$1; ((n%2))&&echo $n || echo -e "\t$n"; let "n=(n%2==0) ? n/2 : 3*n+1,__=n,n==1"; }
n=27; while ! f3n1 $n; do n=$__; done
```

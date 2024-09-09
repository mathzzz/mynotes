# 为ssh服务添加ip白名单
+ 直接在INPUT链中添加
```
iptables -A INPUT -s <src-ip> --dport 22 -p tcp -j ACCEPT
iptables -A INPUT -s <src-ip2> --dport 22 -p tcp -j ACCEPT
...
iptables -A INPUT -s 0.0.0.0/0 -p tcp --dport 22 -j DROP 
```

+ 如果ip过多，可以新建白名单链
```
iptables -N IpWL4ssh 
iptables -A IpWL4ssh -s <src-ip1> -p tcp --dport 22 -p tcp -j ACCEPT
iptables -A IpWL4ssh -s <src-ip1> -p tcp -m multiport --dports 22 -p tcp -j ACCEPT
iptables -A IpWL4ssh -s <network/masklen> --dport 22 -p tcp -j ACCEPT
iptables -A INPUT -j IpWL4ssh
iptables -A INPUT -s 0.0.0.0/0 -p tcp --dport 22 -j DROP
```

+ 常用规则备份
```
iptables -N IpWL4ssh 
iptables -A IpWL4ssh -s 161.117.250.195,124.70.1.14,192.168.0.0/16 -p tcp  --dport 22  -j ACCEPT
iptables -A IpWL4ssh -s 106.63.1.10,36.112.0.0/16 -p tcp  --dport 22  -j ACCEPT

iptables -N IpWL4rdesk
iptables -A IpWL4rdesk -s 192.168.0.0/16 -p tcp -m multiport --dports 33892,63891,63892,63893,63894  -j ACCEPT
iptables -A IpWL4rdesk -s 106.63.1.10,36.112.0.0/16,223.160.0.0/16 -p tcp -m multiport --dports 33892,63891,63892,63893,63894  -j ACCEPT

iptables -N IpWL4gpt
iptables -A IpWL4gpt -s 106.63.1.10,161.117.250.195,124.70.1.14,36.112.0.0/16,192.168.0.0/16 -p tcp -m multiport --dports 60001,62001,62002  -j ACCEPT

iptables -N drop_if_dport
iptables -A INPUT -j drop_if_dport
iptables -A drop_if_dport -s 0.0.0.0/0 -p tcp -m multiport --dport 22,33892,63891,63892,63893,63894,60001 -j DROP

#iptables -A INPUT -s 0.0.0.0/0 -p tcp -m multiport --dport 22,33892,63891,63892,63893,63894,60001 -j DROP
```


# 为ssh服务添加黑名单链 
+ 当登录源随机时，面对一些可疑的ip，添加黑名单规则
```
iptables -N IpBL4ssh 
iptables -A IpBL4ssh -s <src-ip1> --dport 22 -p tcp -j DROP
iptables -A IpBL4ssh -s <network/masklen> --dport 22 -p tcp -j DROP
iptables -I INPUT -j IpBL4ssh
```

# 删除IpWL4ssh中的某条规则
``` shell
iptables -L IpWL4ssh --line-numbers
iptables -D IpWL4ssh 2
```

# 清空IpWL4ssh所有规则
``` shell
iptables -F IpWL4ssh
```

# 删除IpWL4ssh链
``` shell
iptables -X IpWL4ssh
```

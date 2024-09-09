# 1、删除自定义链
iptables -L --line-numbers 查看策略的序号
iptables -D INPUT 规则行  删除被默认链所引用规则
iptables -F in_test_rule 清空才能删除
iptables -X in_test_rule

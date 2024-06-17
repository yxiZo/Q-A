# Q-A
碰到的问题, 以及解决方案的存档


1. 关于 github clone 代码失败的问题

```shell
kex_exchange_identification: Connection closed by remote host
Connection closed by 198.18.0.183 port 22
fatal: Could not read from remote repository.
```

首先排除是操作的问题, 本地生成的ssh key 已经存到了 github 账户中, 如果是这个问题根据官方文档自行排查

根据我的网络环境, 我推测是代理的问题, 因为大部分机场会禁用22端口的通信(应该, 只是推测没有证明)

根据搜索的结果, 找到了这个 issue https://github.com/vernesong/OpenClash/issues/2074

ssh 默认是在 22 端口通信, 

所以根据 github 的 文档测试
```shell
ssh -T git@github.com // failed

ssh -T -p 443 git@ssh.github.com // success

git clone git@ssh.github.com:443:yxiZo/python_tutorial.git // success
```

文档整理: 
  [using-ssh-over-the-https-port](https://docs.github.com/zh/authentication/troubleshooting-ssh/using-ssh-over-the-https-port)

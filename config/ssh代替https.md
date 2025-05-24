# ssh密钥代替https连接

## 意义
因网络问题导致认证失败，
错误如下：
> Failed to connect to github.com port 443 after 21124 ms: Couldn't connect to server


## 完整设置流程

1. 生成ssh密钥
> ssh-keygen -t ed25519 -C "your_email@example.com"

执行后会显示：

> Enter file in which to save the key (~/.ssh/): 
> Enter passphrase (empty for no passphrase):

设置保存的路径和设置密钥密码即可。注：密钥会默认存在id_ed25519,公钥存在id_ed25519.pub.

2. 将公钥添加至github
- 复制公钥
> cat ~/.ssh/id_ed25519.pub

- 登录github-> settings -> ssh and GPG keys -> new ssh key -> 粘贴

3. 切换远程仓库协议
> git remote set-url origin git@github.com:owner/repo.git

注：其中owner为当前用户名，repo为ip地址。可执行whoami，hostname -I等查询。

4. 测试连接
>ssh -T git@github.com
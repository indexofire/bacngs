# BEAST2

## Molecular Clock



## Prior Selection

贝叶斯法分析序列数据时，先验（priors）扮演着非常重要的角色。如果 priors 设置不正确，会导致计算收敛花费非常多的时间，甚至无法收敛，或者对建树产生较大的偏离。

正确选择 priors 和初始值比较困难，



## 手动添加 addon

因为 addon 仓库放在 [github/BEAST2-Dev](https://github.com/BEAST2-Dev) 上，而 [github](https://github.com) 静态文件储存在 [amazonaws](https://aws.amazon.com) 服务器中，由于网络的原因，只有通过代理才能安装插件。如果有 VPN 工具可以直接通过 VPN 加密隧道安装，如果只有 socks5 代理，可以用 proxychains4 配合命令行工具 addonmanager 来安装。如果没有代理，则要分别下载相应的安装包解压缩到 addon 路径中。用户级 addon 安装在 `$HOME/.beast2/` 路径中，系统级的安装在 `/usr/local/share/beast2` 路径中。

```bash
# 安装插件
$ addonmanager -add BDSKY
# 通过proxy安装BDSKY
$ proxychains4 addonmanager -add BDSKY
```

## 参考资料

1. http://treethinkers.org/
2. https://taming-the-beast.github.io/

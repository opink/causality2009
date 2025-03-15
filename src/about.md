# 关于
> 2025-03-14

##  0. 在GitHub Pages上部署MDBook
[如何利用Github Action部署mdBook](https://root-hbx.github.io/carrot-world/BLOG/Markdown/mdbook-site/)
这里我们不走官网提供的流程，因为它会涉及到本地与远端的不同处理。  
我的方案能够保证开箱即用，本地和远程都 work well :))

## 1. 在CloudFlare Pages上部署MDBook
[基于Cloudflare部署网页](https://root-hbx.github.io/carrot-world/BLOG/Markdown/cloudflare/)

现在CF Pages文档不再声称支持mdBook构建了。  
不过按本篇直接下载二进制构建的方法，也可以在CF Pages上使用mdBook。

有人对此提出了一个[issue](https://github.com/cloudflare/cloudflare-docs/issues/885)，里面提到可以试试追加环境变量MDBOOK_VERSION。但issue下面也有人表示加了不管用。

最后的一个workaround是直接把二进制下下来build，真的有用。

将构建命令设为 `curl -L https://github.com/rust-lang/mdBook/releases/download/v0.4.47/mdbook-v0.4.47-x86_64-unknown-linux-gnu.tar.gz | tar xvz && ./mdbook build` （这里注意选择合适你的mdbook版本）

输出目录设为book，

于是就可以构建了。

## 2. 开发团队保重自救
[Predmet Chen's Blog  -  开发团队重保自救](https://predmet.ch/infosec/dev_in_a_hw)


***
引流标签：Judea Pearl, Causality, 因果论, Causal Inference, 因果推断, Reinforcement Learning, 强化学习, 
# 服务器shell使用小tips

> 2025-03-21

## 0. 配置ssh免密登录
用账号和密码来登陆服务器这样很 **不安全**，也许会有一些途径让别人探到你的密码。  
一种更安全的方式是使用 **密钥** 进行登陆：

弱密码会导致黑客能够轻而易举从 SSH 入侵服务器，但是每次登录输入复杂密码会很烦，怎么办呢？其实，SSH 提供了一种相当方便、简单、安全的连接方式：密钥认证。  
它的原理是，用户生成一对密钥，将公钥放在服务器上，登录时 SSH 自动使用私钥认证，两者相符则允许用户登录。

![ssh密钥登录](./img/ssh.jpg)

### 0.1. 在自己的机器上使用 ssh-keygen 生成密钥：
```Bash
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ustc/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ustc/.ssh/id_rsa
Your public key has been saved in /home/ustc/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:/+4tXnjnilyLQvwa+qEKx0IK2jOzHRj0Nbarr3Vot1E ustc@ustclug-linux101
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|                 |
|  .   +          |
| . . o o         |
|. . o . S.E      |
|.o = . o oo  .   |
|. B + B +.+.. + .|
|   * O o =.=oB + |
|  . +oo.+.o*O.+..|
+----[SHA256]-----+
```
#### 上面调用`ssh-keygen`命令后第三步的 *passphrase* 是密钥的密码，设置之后即使私钥被别人拿到也无法使用，可以不输入。最终得到的 id_rsa 是私钥（千万不要分享给别人！），id_rsa.pub 是公钥（可以公开）

### 0.2.在本地使用 ssh-copy-id 命令将公钥拷贝到服务器上：
```Bash
$ ssh-copy-id ustc@localhost
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
ustc@localhost's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'ustc@localhost'"
and check to make sure that only the key(s) you wanted were added.
```

#### 如果服务器不允许使用密码登录，可以将用户目录下的公钥 `.ssh/id_rsa.pub` 文件的 *内容* 全部复制到机器对应用户的 `.ssh/authorized_keys` 文件中

### 0.3. 配置完成后，可以考虑关闭 SSH 服务器的密码验证。做法是编辑 /etc/ssh/sshd_config 文件，进行如下修正：
```Bash
#PasswordAuthentication yes                 ( origin )
->
PasswordAuthentication no                   (  now  )
```
#### 建议: 除非有特殊原因，否则所有正式生产环境服务器（例如实验室服务器）都应该进行如上设置 *关闭 SSH 密码验证*

### 0.4. 让 SSH 服务器重新加载配置
```Bash
$ sudo systemctl reload ssh
```

## 1. ssh远端用tmux保活
在 Linux上执行很多任务，都是需要花时间的，比如几个小时？或者你需要一个程序 / 脚本24h运行；  
但你用ssh连接到服务器，如果我们退出服务器，当前的对话(session，当前开启的shell)就会被终止。  
如果我们希望退出服务器的时候，服务器的任务能够继续执行，我们需要用 tmux :

```bash
$ tmux new -s <session-name> # 新建会话
$ tmux detach # 分离会话（并未结束）（⌃B d）
$ exit # 结束会话（⌃D）

$ tmux ls # 查看当前所有的会话
$ tmux attach -t <session-name> # 接入会话

$ tmux kill-session -t <session-name> # 杀死会话
```

## 2. apt安装程序管理
apt是 Linux服务器上的包管理工具(apt, Advanced Packaging Tool, 是 Ubuntu 自带的包管理工具)。  
我们在 Linux中使用的都是命令行程序，那么如何安装这些命令行程序呢？  
安装一些程序的时候它有相当多的依赖（即这个程序要调用其他的命令行程序），怎么管理这些呢？  
都用包管理工具就好了。  

- apt常用命令：
  - apt update：更新软件源中的所有软件列表，建议在执行安装或更新操作前，先执行该指令。
  - apt list：列出所有软件包
  - apt list --upgradable：列出所有可供更新的软件包
  - apt upgrade：升级软件包
  - apt install <package_name>：安装软件包
  - apt remove <package_name>：卸载软件包
  - apt purge <package_name>：清除软件包（包含软件包和它的配置文件）
  - apt search <package_name>：搜索软件包
  - apt show <package_name>：显示软件包的信息

- apt的几个缺省路径：
  - 下载的软件存放位置：/var/cache/apt/archives
  - 安装后软件默认位置：/usr/share
  - 可执行文件位置：/usr/bin
  - 配置文件位置：/etc
  - 库文件位置：/usr/lib

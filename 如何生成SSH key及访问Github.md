> 操作环境为 Mac os，如果你是 Windows 请出门左转。

一、检查 SSH key 是否存在

在终端输入：

>  ls -al ~/.ssh

如果没有，终端显示如下：

> No such file or directory

如果已经存在，则会显示 id_rsa 和 id_rsa.pub

在终端输入：

> ssh-keygen -t rsa -C "your_email@example.com"

其中 your_email@example.com 为你在 GitHub 注册时的邮箱

成功后终端显示如下：

> Generating public/private rsa key pair.

> Enter file in which to save the key (/Users/xxx/.ssh/id_rsa):

提示你保存 .ssh/id_rsa 的路径，这里直接 enter

> Created directory '/Users/xxx/.ssh'.

> Enter passphrase (empty for no passphrase):

提示输入 passphrase，每次与 GitHub 通信都会要求输入 passphrase，以避免某些「失误」，建议输入

成功后终端显示：

> Your identification has been saved in /Users/xxx/.ssh/id_rsa.

> Your public key has been saved in /Users/xxx/.ssh/id_rsa.pub.

> The key fingerprint is:

> 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48 your_email@example.com

> The key's randomart image is:（后面图形省略）

三、添加 key 到 SSH

输入命令：
> ssh-add ~/.ssh/id_rsa

此时会要求输入 passphrase，输入步骤二中填的 passphrase

成功后，终端显示：

> Identity added: /Users/xxx/.ssh/id_rsa (/Users/xxx/.ssh/id_rsa)

最后，在 /Users/xxx/.ssh/ 生成两个文件，id_rsa 和 id_rsa.pub

此时，SSH key 已经生成成功

四、添加 SSH key 到 GitHub

1.复制 id_rsa.pub 中的所有内容

打开 id_rsa.pub，终端命令：

> vim ~/.ssh/id_rsa.pub

手动复制以 ssh-rsa 到以 your_email@example.com 结尾的所有内容

或者直接输入命令复制 id_rsa.pub 中的所有内容，终端命令：

> pbcopy < ~/.ssh/id_rsa.pub

2.登录 GitHub

打开个人 Settings-->SSH keys-->Add SSH key

Title 随便写

Key 粘贴之前复制的内容

这样 SSH key 就添加的 GitHub

五、检测 SSH key

输入命令：

> ssh git@github.com

此时会验证 SSH key 是否可以访问 GitHub

成功显示如下：

> Hi your_name! You've successfully authenticated, but GitHub does not provide shell access.

Connection to github.com closed.

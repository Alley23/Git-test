### 1. 确认自己是否已经拥有密钥
为了向 Git 服务器提供 SSH 公钥，如果某系统用户尚未拥有密钥，必须事先为其生成一份。 这个过程在所有操作系统上都是相似的。 首先，你需要确认自己是否已经拥有密钥。 默认情况下，用户的 SSH 密钥存储在其 ~/.ssh 目录下。 进入该目录并列出其中内容，你便可以快速确认自己是否已拥有密钥：
```
$ cd ~/.ssh
$ ls
authorized_keys2  id_dsa       known_hosts
config            id_dsa.pub
```
### 2. 生成SSH key 
我们需要寻找一对以 id_dsa 或 id_rsa 命名的文件，其中一个带有 .pub 扩展名。 .pub 文件是你的公钥，另一个则是私钥。 如果找不到这样的文件（或者根本没有 .ssh 目录），你可以通过运行 ssh-keygen 程序来创建它们
```
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/schacon/.ssh/id_rsa):
Created directory '/home/schacon/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/schacon/.ssh/id_rsa.
Your public key has been saved in /home/schacon/.ssh/id_rsa.pub.
The key fingerprint is:
d0:82:24:8e:d7:f1:bb:9b:33:53:96:93:49:da:9b:e3 schacon@mylaptop.local
```
首先 ssh-keygen 会确认密钥的存储位置（默认是 .ssh/id_rsa），然后它会要求你输入两次密钥口令。如果你不想在使用密钥时输入口令，将其留空即可。

### 3. 查看key
```
cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC+X1iMFBvyEE3WJQ/SMHsrC8hVxoWa4XIZtybbKnLsgA3UPJHYN66AU7uvfy9JAGQNaxV4T8JBQGoVy+7of8LklhOLXeLu4hvUnw4dyCEVZXLmM/rGGfHHvaJ8jqmq46NYzq25pIbxkAGhgfOnxYZuDBxdKwBXuhMxXiqDL7SKSNpiV5AJ8/wvX9wLDw5rd2sanjUvOEGzVXlYxMXIss97TVWajSYubkGbIrMrYHmRWRa95UXuhCja8yFE1Hp0Vk8UxpZ0AU677v+Jj6p4fSVEGe8AzgETdQUQcgQk6C6lRj7KC8/BmRGrB0DdfimPjiCcXeJoFsUcG6w9dtE4wGVL wb-likai@cai-inc.com
```

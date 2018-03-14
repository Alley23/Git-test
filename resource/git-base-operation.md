### 克隆、新建、删除分支
- 克隆仓库
```
git clone XXX
```
- 新建并切换到本地分支
```
git checkout -b XXX
```
- 本地代码合并到远程分支
```
git push origin XXX
```
- 拉取运程分支
```
git pull origin XXX
```
- 查看分支
```
git branch -a  //查看远程分支
git branch     //查看本地分支
```

- 切换到分支
```
git checkout XXX
```
- 删除分支
```
git branch -d XXX              //删除本地分支
git push origin --delete XXX   //删除远程分支
```



### 项目提交操作
- 添加项目到暂存区（stage）

```
$ git add .
```
- 查看状态

```
$ git status
```
- 将暂存区中所有修改提交到分支仓库中

```
$ git commit -m "XXX"
//-m 后面紧跟着的是对当前版本的一段描述话语，方便以后再分支仓库中快速找到某个版本；
//注意：这里要用双引号，不能用单引号
```
### 查看版本日志信息
- 查看某个分支仓库中的版本信息

```
$ git log
//commit：每创建一条版本信息时，都会用 SHA1 生成一个很大的数字，并用十六进制进行表示，目的是根据这个 commit id可以找到对应的版本信息，不会重复。
//Author：提交这条版本信息的人是谁，适用于团队开发时，记录每个版本是谁提交的，这样出了问题也好找对应的负责人解决问题。
//Date：这个就是提交到分支仓库的时间了。
//版本描述信息，如果没有它，你看到的只是一大串数字，压根不知道这条版本到底做了哪些修改。
```
- 感觉日志信息输出太多，可以使用 git log --pretty=oneline 在一行显示日志

```
$ git log --pretty=oneline
//输出
ad489d062e14dfe87d0d611e0a98f4345eaa7305 (HEAD -> master, origin/master, origin/HEAD) [02]commit add flie
5792db2ce7891a5b5973d2b1fadce523fbcc7a7c [01]commit test flie
5a5c7081f9bcc077477d6181f7a6a6c2eac522d9 Initial commit
```

### 回滚到指定版本
- 使用 git reset --hard <commit id> 指令进行版本回滚

```
$ git reset --hard 5792db2c

//说明：
//--hard后面跟着的字符串是要回滚到的那条版本信息对应的 commit id，当然不需要全部写，只需要截取前面7-8位唯一标识即可。
```
- 使用 git reflog 指令查看刚才所有操作日志

```
$ git reflog
```
#### git log 与git reflog 区别
- git log：只查询文件修改/新增/删除等与文件有关的日志记录；
- git reflog：不仅记录与文件有关的记录，还会记录对分支仓库的回滚记录。
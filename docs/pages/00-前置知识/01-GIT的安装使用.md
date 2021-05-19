# GIT的安装及使用
## 认识GIT
Git是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理

### 常用GIT平台
github、gitlab、gitee等

### GIT工具安装
##### Windows版下载：
32-bit Git for Windows Setup：[下载地址](https://github.com/git-for-windows/git/releases/download/v2.31.1.windows.1/Git-2.31.1-32-bit.exe)

64-bit Git for Windows Setup：[下载地址](https://github.com/git-for-windows/git/releases/download/v2.31.1.windows.1/Git-2.31.1-64-bit.exe)

##### Mac版下载：
64-bit Git for Mac Setup：[下载地址](https://nchc.dl.sourceforge.net/project/git-osx-installer/git-2.15.0-intel-universal-mavericks.dmg)

##### GIT配置
由于git是分布式管理工具，需要输入用户名和邮箱以作为标识，因此，在命令行输入下列的命令：
```
# 设置用户名
git config --global user.name "Laughing小石头"
# 设置邮箱
git config --global user.email "991107056@qq.com"
```
建议：此处设置的用户名和邮箱建议与你在用的git平台所注册的用户名和邮箱一致

### GIT与其他版本管理工具的对比
这里的其他版本管理工具主要指SVN

SVN：SVN是集中式版本控制系统，版本库是集中放在中央服务器的，而干活的时候，用的都是自己的电脑，所以首先要从中央服务器哪里得到最新的版本，然后干活，干完后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，如果在局域网还可以，带宽够大，速度够快，如果在互联网下，如果网速慢的话，就郁闷了。

GIT：GIT是分布式版本控制系统，那么它就没有中央服务器的，每个人的电脑就是一个完整的版本库，这样工作的时候就不需要联网了，因为版本都是在自己的电脑上。既然每个人的电脑都有一个完整的版本库，那多个人如何协作呢？比如说自己在电脑上改了文件A，其他人也在电脑上改了文件A，这时，你们两之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

### GIT常用命令
1. 版本库克隆（下载代码）
```
git clone 版本库地址
```
2. 版本库创建
```
git init
```
3. 将文件提交到暂存区
```
# 添加单个文件
git add 文件名
# 添加所有文件
git add *
```
4. 将暂存区文件提交到仓库
```
git commit -m "说明文字"
```
5. 将本地仓库和线上空仓库关联
```
git remote add origin 线上仓库地址
```
6. 将本地仓库的内容推送到线上
```
# 如果是第一次推送master分支时需要加上 -u 参数，Git会将本地的master分支内容推送的远程新的master分支，还会把两个master分支关联起来，在以后的推送或者拉取时就可以简化操作
git push -u origin master
# 简化操作
git push
```
7. 拉取线上最新代码
```
git pull
```
8. 版本冲突解决
```
# 回退到上一个版本
git reset --hard HEAD^
# 获取历史版本号
git reflog
# 回退到该版本号对应的版本
git reset --hard
```
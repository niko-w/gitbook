### 根据tag创建新分支

gateway需要建立紧急修复，需要根据tag1.2.2\_1建立分支hotfix-1.2.2\_2

```
git origin fetch //获得最新
git branch hotfix-1.2.2_2 1.2.2_1 //git branch <new_branch_name> <tag_name>
git checkout hotfix-1.2.2_2  //切换到新分支上
git push origin hotfix-1.2.2_2  //将本地创建的分支推送到远程上，现在远程上也会有新的分支了

简单步骤：
git origin fetch
git checkout -b hotfix-1.2.2_2 1.2.2_1
git push origin hotfix-1.2.2_1

```

### 打标签tag

以gateway的紧急修复版本hotfix-1.2.2\_2为例

```
git branch //查看本地分支
git branch -r  //查看远程分支
git branch -a  //查看所有分支
```

![](/assets/QQ截图20160923161423.png)

##### 1.切换到当前要打标签的分支上

`git checkout hotfix-1.2.2_2`

##### 2.拉取远程最新内容到本地分支

最重要的，要先pull，让本地分支上的内容和远程上同的内容保持一致
`git pull`
或者使用工具TortoisetGit上的pull来拉取（我使用的是这种，感觉他更靠谱一点）

**疑问：**
在git bash中git pull之后，再使用工具TortoisetGit上的pull，不会显示是最新的，而是会在pull一次？？
说明在git bash中的pull没有更新到本地

##### 3.打标签，并查看

```
git tag -a 1.2.2_2 -m 'gateway版本1.2.2_2'//打标签1.2.2_2
git tag //查看有哪些分支
git show 1.2.2_2//查看新打的分支的内容，是否与远程分支上一致
```

![](/assets/QQ截图20160923163108.png)
![](/assets/QQ截图20160923163415.png)

##### 4.推动标签到远程分支

`git push origin 1.2.2_2`
![](/assets/QQ截图20160923163754.png)

##### 5.在远程仓库上查看新打的分支

![](/assets/QQ截图20160923163958.png)

### 删除tag

如果打完标签后，发现有错误，即使已经推送到远程后，也可以删除标签

```
git tag -d 1.2.2_2 //删除刚刚打的本地标签
git push origin :refs/tags/1.2.2_2  //删除远程的标签 
```

事实上Git 的推送和删除远程标签命令是相同的，删除操作实际上就是推送空的源标签refs：
`git push origin 标签名`
相当于
`git push origin refs/tags/源标签名:refs/tags/目的标签名1`

### 合并删除分支

以gateway的紧急修复版本hotfix-1.2.2\_2为例
当在分支hotfix-1.2.2\_2上打完标签后，需要将次分支合并到稳点分支master上，并且删除此分支

##### 1.查看现有的分支，并切换到master分支上

```
git branch
git branch -r
git branch -a
git checkout master
```

![](/assets/QQ截图20160923164614.png)

##### 2.合并分支hotfix-1.2.2\_2到master分支

![](/assets/QQ截图20160923164750.png)

##### 3.将本地master分支推送到远程

**重要**步骤2合并之后，只是将本地分支的内容合并到本地master分支上，而远程上的master分支并没有更新，所以需要将本地master分支推动到远程
`git push origin master`
![](/assets/QQ截图20160923165014.png)

##### 4.删除本地分支和远程分支

```
git branch -d hotfix-1.2.2_2 //删除本地分支
git push origin :hotfix-1.2.2_2  //删除远程分支
```

![](/assets/QQ截图20160923165528.png)


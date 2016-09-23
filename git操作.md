### 打标签

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

##### 3.打分支，并查看

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

##### 5.在远程厂库上查看新打的分支

![](/assets/QQ截图20160923163958.png)

### 合并删除分支


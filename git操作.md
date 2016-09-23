####打标签

以gateway的紧急修复版本hotfix-1.2.2_2为例
```
git branch //查看本地分支
git branch -r  //查看远程分支
git branch -a  //查看所有分支
```
![](/assets/QQ截图20160923161423.png)

切换到当前要打标签的分支上
`git checkout hotfix-1.2.2_2`

最重要的，要先pull，让本地分支上的内容和远程上同的内容保持一致
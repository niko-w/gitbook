# 本地代码回退

```
git reset --hard commit-id              回滚到commit-id，讲commit-id之后提交的commit都去除
git reset --hard HEAD~3    将最近3次的提交回滚
```

# 远程代码回滚

```
git log --pertty=online
git reset --soft commit-id
git stash
git push -f
```

## 第1行：**git log 查看提交历史，然后找到要回滚的版本**。历史如下

```
$ git log --pretty=oneline
01bfeae87731292d457bae7bb80d65ec38c9ee40 UDAL-410 DBProxy权限DDL语句解析
4d9d13d2ee7f8c816d6fc92767388c5e1db5d453 UDAL-410 DBProxy权限DDL语句解析
aae9856e4dae23548ed26baff8743b66876fe8f1 profile后发现com.ctg.udal.sql.parse.Uda lMySqlStatementParser.resetParser方法占用了大约13%的CPU 其原因是每次调用这个方法 的时候， 都会用反射获取SQLParser的lexer字段 于是使用静态全局字段直接将这个字段缓 存起来 修改后压测性能上升，CPU使用下降
d926ff33200334f56e89b1c0046937891566215f seq ddl解析
06d147ae63f3ad9068c7710b676690464a731b5d change version to 1.5.0-SNAPSHOT
7c82fcb633f81e49661f7cedc8ad0de970c7332b 全局序列
8f5c198f24353bbfe123e5a0c610333854e3a9a6 全局序列
842c6dd319d0fec5b469eac53395d149dbe94f59 1.0.2-SNAPSHOT->1.3.1-RELEASE
d75bcb246f665dd0dca52722b1cec6c9e77f57f2 扩展词法解析器，可以获取到注释。
```

## 第2行：输入对应版本就行

```
 git reset --soft d926ff332
```
撤销到某个版本之前，之前的修改退回到暂存区（不懂看漂亮的图哦~）。soft 和 hard参数的区别就是，hard修改记录都没了，soft则会保留修改记录。

![](/assets/2-1024x831.png)

① 工作区：就是我们操作的目录

② 暂存区：操作目录的快照

③ 本地版本库：Git的精髓，人人都是中央仓库。也就是Git分布式的好处，自然对比SVN这种集中式

④ 远程版本库：Github这种中央仓库，可以达到共享。

常用的操作也如图所示，不言而喻了。

## 第3行：暂存为了安全起见

## 第4行：覆盖 -f
将本地master push到远程版本库中。**-f 强制覆盖**

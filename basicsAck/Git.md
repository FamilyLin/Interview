1、Git配置：

```shell
git config --global user.name 'your_name'
git config --global user.email 'your_eamil'
```

2、config的作用域

```shell
git config --local  >>>>>只对某个仓库有效(默认)
git config --global >>>>>对当前用户所有仓库有效
git config --system >>>>>对系统所有登录的用户有效

显示配置，加--list
git config --list --local
git config --list --global
git config --list --system
```

3、建Git仓库

```shell
//把已有的项目代码纳入Git管理
cd 项目代码所在文件夹
git init
```

```shell
//新建的项目直接用Git管理
cd 某个文件夹
git init your_project #会在当前路径下创建和项目名称同名的文件夹
cd your_project
```

```shell
//可以在仓库中进行配置user.name user.email
git config --local user.name 'XX'
git config --local user.email 'xx'
```

4、工作区和暂存区

```shell
git add readme.txt
//git add -u  >>>>>一起提交到暂存区
git commit -m'add readme'
```



5、重命名

```shell
mv readme.txt readme.md  //重命名
git add readme.md  //添加到暂存区
git rm readme.txt  //从暂存区和工作区删除

//可以直接使用
git mv readme.txt readme.md //直接在暂存区和工作区同步
```

6、查看日志

```shell
git log   //查看完整日志
git log --oneline //列表形式
git log -n2  //最近的两条日志
git log --all  //查看所有分支日志
git log --graph  //图形化界面
git log branchName //查看指定分支日志
```

```shell
gitk    >>>>>>>>查看版本更新的图形化界面
```

7、查看分支

```shell
git branch -v  >>>>>>查看分支
cat HEAD   >>>>>>>>查看正在工作的分支
git checkout branchName  >>>>>>>>切换分支
git checkout -b branchName >>>>>>创建并切换分支

git diff commit1ID connit2ID >>>>>>>查看两个commit间的区别
git diff --cached >>>>查看暂存区和HEAD之间的区别
git diff  >>>>>>>>默认比较工作区和暂存区之间的差别
git diff -- fileName  >>>>>比较指定文件再工作区和暂存区中的差别


git branch -d branchName >>>>>删除分支
git branch -D branchName >>>>>删除分支（强制）

git reset --hard commitID >>>撤销commit返回到指定commit的状态
```



8、查看commit类型及内容

```shell
git cat-file -t commitID  >>>>>查看type
git cat-file -p connitID  >>>>>查看内容
git commit --amend >>>>修改最近的commit的message
git rebase -i commitID  >>>>>>修改指定commit的message

/*合并多个commit
git rebase -i commitFatherID
将被合并的commit前的命令改为s
*/

git reset HEAD  >>>>>>撤销暂存区中的变更
git reaet HEAD -- fileName >>>>撤销指定文件在暂存区的变更
git checkout -- fileName >>>>撤销工作区的操作，恢复成暂存区内容


```

9、挂起当前工作

```shell
git stash >>>>>>挂起当前工作，挂起后，status不显示
git stash list  >>>>查看挂起的工作（栈）
git stash apply >>>>弹出挂起工作，但不在栈中删除
git stash pop   >>>>弹出挂起工作，并在栈顶删除
```



10、与GitHub连接

```shell
在GitHub中新建repository后，复制ssh,新增远端站点
git remote add github(repository名称) sshID
git remote -v >>>>>>查看远端站点
git push github(远端站点名称)
```




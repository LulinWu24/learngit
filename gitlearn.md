# git入门

`git init`:初始化仓库

`git add readme.txt`：把文件添加到仓库，只是把文件提交到了你本地电脑上的 Git **暂存区**（Staging Area）。你的文件此时连本地仓库都还没正式存入。**可以多次使用，最后commit完成**

`git commit -m "wrote a readme file"`:正是保存到电脑。-m后面的是说明，可以是任意内容。**一定不要忘记-m说明!!!**，说明"说明内容"

`git status`:工作区状态，哪些文件被修改过。

`git diff`:查看修改的内容

修改了文件之后，记得`git add`,`git commit -m "..."`

如果中途终止程序，会生成一个锁文件`index.lock`,使用`remove-Item -Force .git/index.lock`强制删除这个锁文件。或者esc+`:q!`,撤回这个命令。

commit相当于一个快照，一旦文件乱了或者误删了，可以使用commit恢复。

## git回退
```
git log 查看版本
git log --pretty=oneline

git relog  查看所有操作及对应的版本编号
```

`HEAD^`:上一个版本

`HEAD^^`:上上一个版本

`HEAD~100`:往上100个版本

```
git reset --hard HEAD^

cat readme.txt

git reset --hard 1094a
```

**--hard会回退到上个版本已提交状态**
，soft对应的是未提交的状态。

## 工作区与暂存区


**工作区，版本库，版本库又分为暂存区（stage）和分支master(仓库)**

```
git diff  工作区与暂存区的差异

git diff  --cached  暂存区与仓库的差异

git diff HEAD工作区与仓库的差异
```

```
git add 的反向命令：git checkout 撤销工作区修改，把暂存区最新版本转移到工作区

git commit的反向命令：git reset head 把仓库最新版本转移到暂存区
```

如果在工作区修改了，但是没有add,使用checkout把暂存区的转移到工作区

如果已经add了，使用reset把仓库的转移到暂存区，再checkout转移到工作区。

在工作区中用rm删除了文件，如果你确实需要删除`git rm test.txt`，然后再commit；如果是误删的，从版本库里面恢复`git checkout -- test.txt`。

## 远程仓库
添加了ssh key，连接了github

允许添加多个key,有若干电脑，只需把每台电脑的key添加到github，就可以在每台电脑上往gihub推送了。

在github上面创建了一个库。在本地运行命令：`git remote add origin git@github.com:LulinWu24/learngit.git
`,这个远程库的名字就是origin.相当于远程库learngit的别名。

把本地库的所有内容推送到远程库上：`$ git push -u origin master
`

只要本地做了提交，`git push origin master`把本地master分支的最新修改推送至Github.
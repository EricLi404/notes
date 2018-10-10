

不用这个了，换印象笔记。。。。
---------

## git 三个区域 
* 工作区 work dict
* 暂存区 stage
* 分支   master

## `git init`         // 创建版本库（master）
## `git add <file>`    //将改动添加到暂存区（stage）
* git add -A         //添加所有改动
* git add .    // 添加新建文件和修改，但是不包括删除
* git add -u   // 添加修改和删除，但是不包括新建文件

## `git commit  -m "message"`   //将暂存区（stage）中的改动提交到分支（master）
## `git diff <file>`     //查看文件修改的内容
* `git diff`     //是工作区(work dict)和暂存区(stage)的比较 
* `git diff --cached`    //是暂存区(stage)和分支(master)的比较

## `git status`         //查看代码仓库当前状态

## `git reset --hard HEAD^`  // 返回到上个版本
>在Git中，用`HEAD`表示当前版本，也就是最新的提交3628164...882e1，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个^比较容易数不过来，所以写成`HEAD~100`。

* `git reset --head 3628164`
 
>最新的那个版本append GPL已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了，肿么办？

>办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个append GPL的commit id是3628164...，于是就可以指定回到未来的某个版本：

## `git reflog` 
>现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的commit id怎么办？
在Git中，总是有后悔药可以吃的。当你用`$ git reset --hard HEAD^`回退到`add distributed`版本时，再想恢复到`append GPL`，就必须找到`append GPL`的`commit id`。Git提供了一个命令`git reflog`用来记录你的每一次命令：

 ```
$ git reflog
ea34578 HEAD@{0}: reset: moving to HEAD^
3628164 HEAD@{1}: commit: append GPL
ea34578 HEAD@{2}: commit: add distributed
cb926e7 HEAD@{3}: commit (initial): wrote a readme file
 ```
## `git checkout -- file`   //撤销修改
## `git rm`           //删除文件
## `git remote add origin git@github.com:leif-lyy/test.git`  
> 将本地的 git 代码仓库添加到 github 远程仓库 
> origin 为该远程仓库的别名

## `git clone git@github.com:leif-lyy/test.git`   //从远程仓库克隆
## `git branch dev` //创建 dev 分支
```
$  git branch dev  //创建 dev 分支
$  git checkout dev  //切换到 dev 分支
------------
上边的命令等价于：
$  git checkout -b dev  //创建并切换到 dev 分支
```
## `git branch`  //查看当前分支
## `git checkout master`  //切换到 master 分支
## `git merge dev`    //将 dev 分支合并到当前分支
## `git branch -d dev`    //将 dev 分支删除
## `git branch -D dev`     //强行删除一个没有被合并过的分支
## `git log --graph` 查看分支合并图
## `git merge --no-ff -m "merge with no-ff" dev`   
禁用 fast forward 合并 dev 分支到当前分支；
因为这会造成一次 commit ，所以要填写 commit message。

## `git stash`   //储藏当前修改
```
git stash     //将当前修改储藏
git stash list     //查看储藏列表
----------
# 恢复储藏
git stash apply      //恢复但不删除
git stash pop        //恢复并删除
git stash drop       //删除储藏 
```
## `git tag <name>`     //新建标签,默认为 HEAD
```
git tag <name> <commit id>         //给以前的版本打 tag
git tag -a <tagname> -m "messaga"       //指定标签信息
git tag           //查看所有 tag
git show <tagname>    //查看该 tag 的详细信息
-------------
git push origin v1.0         //将1.0标签推送到远程
git push origin --tags        //一次性推送全部尚未推送到远程的本地标签
-------------
如果 tag 已经推送到远程，则删除 tag 需要在本地和远程分别删除 tag
git tag -d   v1.0            //删除本地 tag
git push origin :refs/tags/v1.0   //删除远程 tag
```
## `git checkout . && git clean -xdf`
清除本地所做修改

## .gitignore规则不生效的解决办法

把某些目录或文件加入忽略规则，按照上述方法定义后发现并未生效，原因是.gitignore只能忽略那些原来没有被追踪的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。那么解决方法就是先把本地缓存删除（改变成未被追踪状态），然后再提交：

1. `git rm -r --cached .`
2. `删除要停止追踪的文件`
3. `git add .`
4. `git commit -m 'update .gitignore' `




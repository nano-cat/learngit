# Git 学习笔记

###  1. 基本命令

##### &nbsp;&nbsp;创建Git仓库

* ```
  git init
  ```
  * 把当前目录变成Git可以管理的仓库

##### &nbsp;&nbsp;添加文件到仓库

* ```
  git add
  ```
  * 例如: `$ git add readme.txt` 

##### &nbsp;&nbsp;提交到仓库

* ```
  git commit
  ```
  * 例如: `$ git commit -m "wrote a readme file"`

##### &nbsp;&nbsp;查看仓库当前状态

* ```
  git status
  ```

##### &nbsp;&nbsp; 查看修改内容

* ```
  git diff
  ```
  * 例如: `$ git diff readme.txt`

##### &nbsp;&nbsp; 查看日志

* ```
  git log
  ```

##### &nbsp; &nbsp; 版本回退

* ```
  git reset --hard
  ```
  * 例如: `$ git reset --hard HEAD^` `$ git reset --hard 455c82d`

##### &nbsp;&nbsp; 回退命令记录

* ```
  git reflog
  ```

##### &nbsp;&nbsp; 撤销修改

* ```
  git checkout -- file 
  ```

  * 例如: `$ git checkout -- readme.txt `(查看)

    一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

    一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
  
    总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态
  
* ```
  git reset HEAD <file>
  ```

  * 例如: `$ git reset HEAD readme.txt`

    把暂存区的修改撤销掉（unstage），重新放回工作区

##### &nbsp;&nbsp; 删除文件

* ```
  git rm <file>
  ```
  * 例如: `$ git rm test.txt`  `$ git commit -m "remove test.txt"`

### 2. GitHub远程仓库

##### &nbsp;&nbsp; 第一步: 创建SSH Key

* ```
  ssh-keygen -t rsa -C "youremail@example.com"
  ```

##### &nbsp;&nbsp; 第二步: 添加key

* 在Key文本框里粘贴id_rsa.pub文件的内容

#### 2.1 关联远程库

##### &nbsp;&nbsp; Github添加远程库

* github创建新仓库: 右上角找到“Create a new repo”按钮

##### &nbsp;&nbsp; 关联github远程库

* ```
  git remote add origin git@github.com:nano-cat/learngit.git
  ```

##### &nbsp;&nbsp; 推送到远程

* 第一次:
  * ```
  git push -u origin master
    ```
* 以后只要本地作了提交: 
  * ```
    git push origin master
    ```
#### 2.2 克隆远程库

##### &nbsp;&nbsp; 克隆到本地库

* ```
  git clone git@github.com:nano-cat/learngit.git
  ```

### 3. Git分支管理

#### 3.1 创建与合并分支

* 创建分支

  ```
  git checkout -b dev
  ```

  * 相当于`$ git branch dev`(创建分支) + `git checkout dev`(切换) 

* 查看当前分支

  ```
  git branch
  ```

* 切换回`master`分支

  ```
  git checkout master
  ```

  * Git 提供了新的命令切换分支

    ```
    git switch master
    git switch -c dev //创建并切换
    ```

* 合并分支

  ```
  git merge dev (尽量用--no-ff方式合并)
  ```

  * `git merge`命令用于合并指定分支到当前分支

* 删除`dev`分支

  ```
  git branch -d dev
  ```
  
  * 强制删除未合并分支
  
    ```
    git branch -D dev
    ```

#### 3.2 合并冲突

* 合并冲突 提示`both modified:   readme.txt`

* Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容

* 用带参数的`git log` 查看分支合并情况

  ```
  git log --graph --pretty=oneline --abbrev-commit
  ```

* 用`git log --graph`命令可以看到详细信息的分支合并图

#### 3.3 分支管理策略

* 通常，合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。

  如果要强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

  下面我们实战一下`--no-ff`方式的`git merge`：

  ```
  git merge --no-ff -m "merge with no-ff" dev
  ```

* 在实际开发中，我们应该按照几个基本原则进行分支管理：

  `master`分支应该仅用来发布新版本, 在`dev`分支上干活

#### 3.4 Bug分支

* **"存储"**当前工作区(储存后当前工作区变为最近一次commit时的)

  ```
  git stash
  ```

  * 切换到有bug 的分支
  * 当修改完其他分支的bug后, 回到此前分支

* 查看`stash`的工作区

  ```
  git stash list
  ```

* 恢复工作区
  * 恢复并删除
    ```
    git stash pop
    ```
  
  * 恢复`git stash apply` , 删除`git stash drop` 

#### 3.5 多人协作

* 查看远程库信息

  ```
  git remote -v
  ```

* 推送分支 (分支是否推送看情况而定)

  ```
  git push origin master (主分支)
  git push origin dev    (开发分支)
  ```

* 创建远程`origin`的`dev`分支到本地

  ```
  git checkout -b dev origin/dev
  ```

* 推送冲突(推送失败)

  * 拉取最新提交(有对应的本地分支)

    ```
    git pull
    ```

  * 指定本地`dev`分支与远程`origin/dev`分支的链接(无对应)

    ```
    git branch --set-upstream-to=origin/dev dev
    ```

    解决完冲突后`git push origin dev`

### 4. 标签

#### 4.1 创建标签

* 切换到需要打标签的分支

  ```
  git checkout master
  ```

* 打一个新标签(打在最新提交的commit上)

  ```
  git tag v1.0
  ```

* 查看所有标签

  ```
  git tag
  ```

* 补打标签

  * 找到历史提交的commit id

    ```
    git log --pretty=oneline --abbrev-commit
    ```

  * 打上对应的标签

    ```
    git tag v0.9 
    ```

    
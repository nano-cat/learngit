# Git 学习笔记

###  基本命令

##### &nbsp;&nbsp;创建Git仓库

* `git init`  
  * 把当前目录变成Git可以管理的仓库

##### &nbsp;&nbsp;添加文件到仓库

* `git add`  
  * 例如: `$ git add readme.txt` 

##### &nbsp;&nbsp;提交到仓库

* `git commit`  
  * 例如: `$ git commit -m "wrote a readme file"`

##### &nbsp;&nbsp;查看仓库当前状态

* `git status` 

##### &nbsp;&nbsp; 查看修改内容

* `git diff`  
  * 例如: `$ git diff readme.txt`

##### &nbsp;&nbsp; 查看日志

* `git log`  

##### &nbsp; &nbsp; 版本回退

* `git reset --hard`  
  * 例如: `$ git reset --hard HEAD^` `$ git reset --hard 455c82d`

##### &nbsp;&nbsp; 回退命令记录

* `git reflog`

##### &nbsp;&nbsp; 撤销修改

* `git checkout -- file `

  * 例如: `$ git checkout -- readme.txt `

    一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

    一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

* `git reset HEAD <file>`

  * 例如: `$ git reset HEAD readme.txt`

    把暂存区的修改撤销掉（unstage），重新放回工作区

##### &nbsp;&nbsp; 删除文件

* `git rm <file>` 
  * 例如: `$ git rm test.txt`  `$ git commit -m "remove test.txt"`

### GitHub远程仓库

##### &nbsp;&nbsp; 第一步: 创建SSH Key

* `$ ssh-keygen -t rsa -C "youremail@example.com"`

##### &nbsp;&nbsp; 第二步: 添加key

* 在Key文本框里粘贴id_rsa.pub文件的内容

#### 先有本地库后关联远程库

##### &nbsp;&nbsp; Github添加远程库

* github创建新仓库: 右上角找到“Create a new repo”按钮

##### &nbsp;&nbsp; 关联github远程库

* `$ git remote add origin git@github.com:nano-cat/learngit.git`

##### &nbsp;&nbsp; 推送到远程

* 第一次: `$ git push -u origin master`
* 以后只要本地作了提交: `$ git push origin master`
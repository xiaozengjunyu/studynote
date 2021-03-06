## 2021-04-28 学习内容

>参考
> * [《廖雪峰Git教程》](https://www.liaoxuefeng.com/wiki/896043488029600)  

* [一、分支管理]()
  * [1.创建分支](#1创建分支)
  * [2.合并分支](#2合并分支)  
  * [3.分支冲突](#3分支冲突)
  * [4.分支策略](#4分支策略)
  * [5.bug 分支](#5bug分支)
  * [6.多人协作](#6多人协作)
  * [7.rebase 操作](#7rebase操作)
  * [8.merge 操作](#8merge操作)
* [二、注意点](#注意点)
## 一、分支管理
 分支就是从主线分出来的支线，但这个支线又不影响主线，最后支线完成任务后合并到主线上然后删除支线。  
  ### 1.（创建分支）

#### 示例
    $ git checkout -b dev #创建 dev 分支，并切换该分支  
    Switched to a new branch 'dev' #显示此代码,表示创建成功并切换到 dev 分支  
<font size=2>分支创建完成了我们就需要合并了</font>    

  ### 2.（合并分支）
  首先我们需要切换为 main 分支，用命令指定分支合并当前分支。

#### 示例：
    git merge dev  #将 dev 合并到当前分支
    git branch -d dev #删除dev分支  

合并完成后删除dev分支，主分支不受任何影响

  ### 3.（分支冲突）
 首先分支相当于修改 PPT，你改前几页，他也改前几页，等到要合并的时候，就会发生问题也就是分支冲突。
 
 出现冲突我们可以是用 git status 查看冲突的文件  
 示例：  

    $ git status
    On branch master
    Your branch is ahead of 'origin/master' by 2 commits.
      (use "git push" to publish your local commits)
    
    You have unmerged paths.
      (fix conflicts and run "git commit")
      (use "git merge --abort" to abort the merge)
    
    Unmerged paths:
      (use "git add <file>..." to mark resolution)
      	both modified:   readme.txt
    no changes added to commit (use "git add" and/or "git commit -a") 
  Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容

  ### 4.（分支策略）
  一个项目 main 主分支，肯定不可能在主分支干活，我们需要从主分支上划分 dev 分支再从 dev 分支上划分分支，于是每个人都有自己的分支，我的分支任务完成后提交到 dev 分支上，没出问题之后再提交到 main 分支。

  ### 5.（bug分支） 
  git 提供了 stash 功能，可以把现场储存起来，等以后恢复现场继续工作：
   #### 示例：
       $ git stash
       Saved working directory and index state WIP on dev: f52c633 add merge
  使用 stash 功能保存现场，需要修复的分支是哪个就，从哪里创建个分支用于修复，修复完成后合并。
  ###  6.（多人协作）
   * 首先，用命令推送我们的修改
   * 如果推送失败，把最新的抓去下来，在本地库合并
   * 合并出现冲突，解决冲突，在本地提交
   * 最后没有冲突或者解决了冲突，然后推送远程库。
  ### 7.（rebase 操作）
   * rebase 的特点：合并的结果呈一条线,好看优美。  
   * rebase 的弊端：如果合并过程出现冲突，可能会出现多个冲突。

  ###  8.（merge 操作）
  * merge 的特点：合并出现冲突，只用解一次就好。    
  * merge 的弊端：合并结果不好看，一堆交错的线。

## 注意点：
  * 在创建的分支操作，切换到主分支是不显示的，只有当分支合并后，才可以显现。
  * 分支合并时有提示信息，出现 Fast-forward 信息，是告诉我们，此次合并是主分支指向 dev 提交的。
  * 分支出现无法合并的时候，我们先找到冲突原因并解决，即可提交合并成功。
  * 使用 stash 功能存储现场，修复合并完成之后，工作现场还存在需要手动删除。
  * 每添加一个新功能，最好新建一个 feature 分支，在上面开发。
  * 尽量及时 rebase 上游分支，发现有冲突，merge。

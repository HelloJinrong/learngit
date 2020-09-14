1. 本地初始化名为learngit的仓库；将该本地仓库推送到个人github中。

   ```shell
   git init learngit
   git add .
   git commit -m "fisrt commit"
   git remote add origin https://github.com/HelloJinrong/learngit.git
   git push origin master
   ```

2. 执行 clone learngit 仓库的 dev 分支到本地;分别使用 switch和checkout命令在本地创建 feature-1 分支并对应到远程该分支。

   ```shell
   git clone -b dev https://github.com/HelloJinrong/learngit.git
   git switch -c feature-1 
   git checkout -b feature-1
   git push origin feature-1
   ```

3. 协同开发所涉及的 git 命令有：

   模拟A在dev分支上完成编写测试文件工作

   ```shell
   git checkout dev
   touch text.md
   echo "this is a test">text.md
   git add .
   git commit -m "test"
   git push origin dev
   ```

   

   模拟B协同完成：

   - 从远程库中克隆
   - 创建远程`origin`的`dev`分支到本地
   - 可以在`dev`上继续修改，然后，时不时地把`dev`分支`push`到远程

   ```shell
   git clone git@github.com:HelloJinrong/learngit.git
   git checkout -b dev origin/dev
   touch text2.md
   echo "this is a test2">text2.md
   git add .
   git commit -m "add test2"
   git push origin dev
   ```

   

   - 如果推送失败，则用`git pull`把最新的提交从`origin/dev`抓下来，然后，在本地合并，手动解决冲突，再推送

   ```shell
   git pull
   ...
   git push origin dev
   ```

   4. 回退两次提交前的版本：`git reset --hard HEAD~2`

      查看提交记录：`git log`

      查看之前的版本号：`git reflog`

      还原到执行回退操作之前的版本:`git reset --hard <版本号>`

   5. ```shell
      git checkout feature-1
      git pull
      git checkout master
      git merge feature-1
      git push
      ```

      

6. 给代码库打 tag，tag 名为v0.1,描述信息为version 0.1 released。并将该 tag 推到远程分支。以及如何删除本地和远程仓库名为 v0.9的 tag。

   ```SHELL
   git tag -a v0.1 -m "version 0.1 released" 
   git push origin v0.1
   git tag -d v0.9
   git push origin :refs/tags/v0.9
   ```

7. ```shell
   git checkout feature-1
   git pull
   git stash
   git checkout dev
   git push origin dev
   git checkout master
   git cherry-pick dev
   git push
   git stash pop
   ```

8. ```shell
   git log --since=2020-04-02 --until=2020-08-06 --author="cheny" 
   ```

9. ```shell
   git reset --hard 01e31c
   ```

10. 如何修改倒数第 5 次（HEAD~5）提交的 message 信息。如果要将此次修改同步到远程仓库，如何操作？应该注意什么，如果不注意会造成什么后果

    `git rebase -i HEAD~5`将`pick`改为`edit` ，` git commit --amend`，

    执行 `git rebase --continue`，最后`git push -f `。要注意如何已经集成到分支上，就不能轻易的使用`rebase`。不然会影响到团队的其他成员。

11. 简述 merge 和 rebase的区别。

    merge和rebase都是用来合并分支的。区别是：

    - 采用merge和rebase后，git log的区别，**merge命令不会保留merge的分支的commit**
    - 处理冲突的方式：
      - 使用`merge`命令合并分支，解决完冲突，执行`git add .`和`git commit -m'fix conflict'`。这个时候会产生一个commit。
      - 使用`rebase`命令合并分支，解决完冲突，执行`git add .`和`git rebase --continue`，不会产生额外的commit。这样的好处是，‘干净’，分支上不会有无意义的解决分支的commit；坏处，如果合并的分支中存在多个`commit`，需要重复处理多次冲突。

12. 简述fetch 分别与 pull和 pull --rebase的区别。

    都是从远程拉取代码到本地，git fetch只是拉取到本地，git pull不仅拉取到本地还merge到本地分支中。所以git pull是git fetch与git merge的集合体。

    git pull = git fetch + git merge
    git pull --rebase = git fetch + git rebase

13. 简述 git 中工作区、暂存区和版本库的区别。

    - **工作区：**就是你在电脑里能看到的目录。
    - **暂存区：**英文叫stage, 或index。一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
    - **版本库：**工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

14. 简述使用 feature 分支模式进行开发的流程中（拉取代码、创建分支、开发完成后合并分支解决冲突）如何使用一些列的 git 命令。（如 pull, commit, merge, add, fetch,push等）

    - git pull 从orgin下载最新的状态到相应的本地分支并合本地分支merge
    - git pull --rebase 从orgin下载最新的状态到相应的本地分支，再应用本地分支的改动。
    - git fetch 从orgin下载最新的状态到相应的本地分支，但不进行merge
    - git add . 把当前的修改添加到本地暂存区
    - git commit -m "" 将暂存区的修改提交
    - git push 推送到远程服务器








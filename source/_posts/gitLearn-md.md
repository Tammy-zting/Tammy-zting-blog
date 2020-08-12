---
title: Git汇总学习
date: 2020-08-05 09:56:06
tags:
---
# Git 学习

## config

- 设置用户名和账号 使用了`--global`参数 表示你这台机器上的所有仓库都会用这个配置

    ```
    git config --global user.name "Your Name"
    git config --global user.email "email@example.com"
    ```

- 查看配置

  ```
  git config --list
  ```

## 创建仓库

- 创建文件夹

  ```
  mkdir learngit
  cd learngit
  ```

- 初始化仓库 初始化后会生成一个`.git`目录，这个目录是隐藏的，不要手动删掉

  ```
  git init
  ```

- 把文件添加到仓库

  ```
  git add yourfile.txt 
  //或者添加所有
  git add .
  ```

- 提交到仓库 `-m`后面输入的是本次提交的说明，输入有意义的说明很重要

  ```
  git commit -m "wrote a yourfile.txt"
  ```

  - 注意`-am`区别

    ```
    git commit -am "xxxxx"
    ```

    可以省略使用git add命令将已跟踪文件放到暂存区的功能，如果是新增的文件，处于未跟踪状态无法提交

  - 为什么git需要`add`和`commit`两步

    ```
    git add file1.txt
    git add file2.txt file3.txt
    git commit -m "add 3 files"
    ```

    因为`commit`可以一次提交很多文件，多次`add`不同的文件

## 仓库操作

### git status 查看状态

- 下面表示`ztt.txt`这个文件被修改过

![](https://note.youdao.com/yws/api/personal/file/7F76757A206345549E1BFB139408AAFB?method=download&shareKey=57da0c3daa5faa757d134d11ddda323b)

### git diff  比较修改

- 顾名思义就是查看文件的对比，我们可以看出第一行增加了`add content`

  ![](https://note.youdao.com/yws/api/personal/file/493E6B4860A449898E40A588E47B5CC8?method=download&shareKey=6a444af3cf44c503fc4d7db849bae7ab)

- 查看完修改的内容就可以放心提交了`git commit -am "add content"`

  ![](https://note.youdao.com/yws/api/personal/file/A2B8C318D9724871A5A486B41BEEA06A?method=download&shareKey=24e70a94e25022887a279a21b7fbbadb)

## git log 查看快照

- 查看快照 即每次`commit`后的内容，从下面可以看出我们做过两次提交,显示的顺序是从近到远

  ![](https://note.youdao.com/yws/api/personal/file/E978D64120874253B6E49D9304CD9527?method=download&shareKey=ff5055da3e134496f2861031b7eea347)

​	

## git reset 撤销

### 撤销已经提交到分支的恢复

- 让我们再修改下文件 增加一行`add footer`,再查看下`git log`

  ![](https://note.youdao.com/yws/api/personal/file/B5B0AEEE7CDB45669F28D8847FD92273?method=download&shareKey=b4b2addc24baa65e6566148d3e1b4acf)

- 方法一 恢复到上一个版本，`~x`代表回退到上几个版本

  ```
  git reset --hard HEAD~1
  ```

  ![](https://note.youdao.com/yws/api/personal/file/FF18BE1316624EAF88A32D2B9FBCD323?method=download&shareKey=4dd1fc5fe921f46a447ecb2a436a9773)

- 方法二 恢复到未来版本 ，只要窗口没关闭的话你可以，往上找到版本号，不用写全，会自动补全（当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。）

  ```
  git reset --hard 版本号xxx
  ```

  ![](https://note.youdao.com/yws/api/personal/file/7314660A6F7A4C5FACD8746FA577F89F?method=download&shareKey=2d87b9956a8f4ae88c855573b241776c)

### 撤销已经提交到暂存区的操作

- 第一步执行 文件会恢复到修改后的工作区 未添加到暂存区状态

    ```
    git reset HEAD yourfile.txt
    ```

    HEAD表示最新的版本

![](https://note.youdao.com/yws/api/personal/file/52CA43863D5A42949381976A5A9405D9?method=download&shareKey=4407a393dd88bb1b6e3579c987d9f28f)

- 第二步 恢复到修改前的文件

      git checkout -- yourfile.txt

## git reflog 查看操作过程

- 用于查找`commit id`，它会记录你的每一次操作

  ![](https://note.youdao.com/yws/api/personal/file/B9E1E715C466492B8E6D1B048A13EEE2?method=download&shareKey=f8910808482d8bb290ac65b7b04602ae)

## 工作区和暂存区

- 工作区：我们存放文件的文件夹，`.git`这个隐藏目录是git的版本库

- git版本库中最重要的称为`Stage`即暂存区，git会为我们自动创建第一个分支`master`,以及指向`master`的一个指针`HEAD`，我们控制版本就是移动这个指针来更新文件

  ![](https://note.youdao.com/yws/api/personal/file/55659E9EB95D4576949F98BC1DEA6557?method=download&shareKey=e56ab0e3080843f27fe1d80a4a1aed0e)

  第一步`git add`就是把文件添加到暂存区

  第二步`git commit`就是把暂存区的内容提交到当前分支

## git checkout -- yourfile.txt 恢复文件

- 情况一 文件自修改后还没被放到暂存区，撤销修改就回到修改前的状态

- 情况二 文件已经添加到暂存区，又做了修改，撤销修改就回到添加到暂存区后的状态

  ![](https://note.youdao.com/yws/api/personal/file/D6C9D2C485DF4CE2B622801C756B42DE?method=download&shareKey=e79245e3061cbe6cc773e1653f9e1646)

  *注意命令中的`--`很重要，如果没有就变成了切换到另一分支的命令*

  

## git rm 删除暂存区的文件

- 对应`git add`的操作 

- 现在工作区新建一个`test.txt`文件，并提交到分支，再在工作区手动删除文件，查看状态

  - 情况一 删除暂存区的`test.txt`文件

    ![](https://note.youdao.com/yws/api/personal/file/ABF2A36A9ACD47CC993A4CE2AAB66D92?method=download&shareKey=6b6627657d0ed079fec330d5bf1a7fa0)

  - 情况二 不小心误删的，因为暂存区还有保存着一份，故可以执行以上的命令恢复文件

    ![](https://note.youdao.com/yws/api/personal/file/D12784CEB09B436B8C8DA8E373E6260C?method=download&shareKey=26f49de005c755f9901d87b830e7ea75)

  

## 远程仓库

### GitHub

  - 本地Git仓库和GitHub仓库之间的传输是通过SSH加密的

    - 创建SSH Key，在用户主目录下（cmd），查看是否存在`.ssh`目录，若没有创建

      ```
      ssh-keygen -t rsa -C "youremail@example.com"
      ```

      ![](https://note.youdao.com/yws/api/personal/file/BB4EFA420A6644039723A7BD8B4D65CF?method=download&shareKey=e22ffd65385f7b5a86b602272db398ff)

    - 之后就可以找到`.ssh`目录，其中`id_rsa`和`id_rsa.pub `两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露，`id_rsa.pub`是公钥，可以放心给别人

    - 登录Github,打开setting,选择SSH and GPG keys ,创建New SSH key

      ![](https://note.youdao.com/yws/api/personal/file/6EA79857D90444E581D52C46ED4918FB?method=download&shareKey=bb6061d702ecf0702c6f81f11aa92e4a)

      ![](https://note.youdao.com/yws/api/personal/file/8EADEBA9761E44A887015116A599E768?method=download&shareKey=9750b7b867b8e9d0f76f3badb161b26e)

    

    ​		Title任意填，Key粘贴公钥里的内容即可`id_rsa.pub `

    

### 添加远程库

  - github创建一个新的Repository

    ![](https://note.youdao.com/yws/api/personal/file/8F3175BF88B84E20873E52B429277FA7?method=download&shareKey=359709298efb9996c1a2fc83fa4a5e89)

  - 然后可以根据github提示来

    ![](https://note.youdao.com/yws/api/personal/file/2288BBBB002A45D490134EC29A8ABCFF?method=download&shareKey=aff2fc1ced59474b188f65e07174a808)

    - 在本地仓库运行命令 注意地址是你自己github的

      ```
      git remote add origin https://github.com/yourgithub/test.git
      ```

      添加后远程库的名字就是`origin`,这是Git默认的叫法，可以换成别的，但是不建议，因为`origin`本意就是远程库

    - 推送本地内容到远程库

      ```
      git push -u origin master
      ```

      用`git push`命令，实际上是把当前分支`master`推送到远程

      由于第一次推送，远程库是空的，所以加上了`-u`，Git会把本地的`master`分支内容推送到远程新的`master`分支，还会把本地`master`分支和远程`mster`分支关联起来，方便以后推送和拉取可以简化命令

    - **之后只要本地做了提交，可以通过以下命令把本地`master`分支最新修改推送到远程库**

      ```
      git push origin master
      ```

      

### git clone xxxx 克隆远程库到本地

  - 地址可以是浏览器上的`https://xxxx`
  - 也可以是SSH的 `git@github.com:xxxx`

## 分支管理

  - 使用场景即多人协作，当你代码还没完成需要提交避免进度丢失，但是提交又会影响其他人开发时，创建自己的分支，这样就不会相互影响，等开发完毕再一次性合并到原来的分支上

### 创建与合并分支

#### 原理

  - `master`分支是一条线，`HEAD`指向`master`，每次提交`master`分支都会向前移动一步，这样随着你不断提交`master`分支线会越来越长

    ![](https://note.youdao.com/yws/api/personal/file/EE272469AC994DD6A5ECA6E1FA5903AC?method=download&shareKey=7a18c12a3103a6e192433bf2ef005afd)
    - 创建`dev`分支，指向`master`相同的提交，`HEAD`指向`dev`,从此对工作区的修改和提交都是针对`dev`分支，比如新提交，`dev`指针会往前移动一步，但是`master`不会移动

      ![](https://note.youdao.com/yws/api/personal/file/51145F6538F54C33ACEEC86CBE782683?method=download&shareKey=3017705c7758aa5a23d3b774d89330ff)

      ![](https://note.youdao.com/yws/api/personal/file/7DACEE0DF83A4D06B797D5D88706C07F?method=download&shareKey=4e611972220915a99f3471386fc6b912)

  - 合并`dev`到`master`，直接把`master`指向当前`dev`提交

    ![](https://note.youdao.com/yws/api/personal/file/205EC3953C454375A4F113D5DEE68690?method=download&shareKey=121d80a3de26aa47d38c84e581730513)

  - 合并完成之后就可以把`dev`分支删除，只剩下`master`分支

    ![](https://note.youdao.com/yws/api/personal/file/49E7A5752E824B79B4B921AE5F978D34?method=download&shareKey=f2b3c546d118cdf57d73170db528674c)

#### 实例

  - 创建并切换分支到新创建的`dev`分支

    ```
    git checkout -b dev
    ```

    上面的相当于执行两句

    ```
    git branch dev
    git checkout dev
    ```

  - 查看当前分支

    ```
    git branch
    ```

    ![](https://note.youdao.com/yws/api/personal/file/6DF637F3E4834C7580F1249FCD9F6308?method=download&shareKey=1c50acd973d232f5d9214dd1f7dada7f)

  - 增加`new.txt`文件，提交到`dev`分支,切换到`master`分支看不到这个文件，这是因为这个文件提交到的是`dev`分支，现在切换到`master`分支做合并分支操作，之后可以删除`dev`分支

    ```
    git checkout master
    git merge dev
    ```

    ![](https://note.youdao.com/yws/api/personal/file/8F403473073C43968226FA38C5DBFE3A?method=download&shareKey=442e6a7e8a6bdfd18690de52559e1bb9)

### 解决冲突

  - 新增并切换到分支`demo`

    ```
    git switch -c demo
    ```

    *由于git checkout 担任角色太多 既要担任切换分支又要担任恢复文件，故用以上代替 git checkout -b demo*

  - 文件`new.txt`中增加一行`A & B`,然后提交到分支

  - 切换到`master`分支，再次修改`new.txt`文件，增加一行`A and B`，然后提交分支

  - 执行`git merge demo`合并分支命令，`git status`会有冲突提示

    ![](https://note.youdao.com/yws/api/personal/file/7EFD2EDF67C148028EE6496FE621AFA9?method=download&shareKey=044ffd460484c4e8c15d4d93b0759c79)

    *其中提示比远程仓库提前了2个提交Your branch is ahead of ‘origin/master’*

    *git merge demo 是采用`Fast forward`模式，禁用该模式可以加参数 git merge --no-ff -m "xxx",加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。*

  - 查看`new.txt`文件，Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，

    ![](https://note.youdao.com/yws/api/personal/file/4EEB409FA1DA4F528AE4D938753C2AF8?method=download&shareKey=5523a5ee217ba0de10d8bff9be8a7794)

  - 修改`new.txt`文件，解决冲突后提交即可，删除`demo`分支
  
    ```
    git branch -d demo
    ```

    *git log --graph --pretty=oneline --abbrev-commit 可以查看分支合并图*

### 保存工作区

  - 应用场景修复bug,但是当前你是处在分支`demo`上处理问题，问题只处理到一半不能提交，但是领导要求你要先修复bug,解决方法如下
  
    - 保存分支`demo`工作区内容,你可以多次保存
    
      ```
      git stash
      ```
    
      ![](https://note.youdao.com/yws/api/personal/file/0090D6C553FE4E939C4EE5DDBF30524C?method=download&shareKey=a185f3b663dea8adff9ad4f3eb364189)
    
    - 切换到`master`,创建并切换到新分支例如`issue-101`，修复bug,切换回`master`直接合并分支
    
    - 切换回`demo`工作区继续干活，首先就要恢复工作区
    
      ```
      git stash list //查看
      
      git stash apply stash@{0}  //恢复指定的位置
      git stash drop //删除
      
      git stash pop //上面两句可以用这句代替
      ```
    
      ![](https://note.youdao.com/yws/api/personal/file/453A5C263E3345328E669538BB96EE3B?method=download&shareKey=f8c84ad48fad2a96345e7043e564f4fc)
    
    - 提交`demo`分支的工作
    
    - 复制`master`刚刚修复的bug
    
      - 这是提交的`master`的bug
    
      ![](https://note.youdao.com/yws/api/personal/file/AE38C2B3BB3D4C07BA8FA406A7199FE1?method=download&shareKey=a0c11153efd74bc77c6cc3724f6acf3d)
    
      - 复制master的bug
    
          ```
          git cherry-pick <commit>
          ```

          ![](https://note.youdao.com/yws/api/personal/file/9E8BA3EE4D2C4A0F9344E354823E087B?method=download&shareKey=b5a5a8aacde793dd5e5db337a60b7ef9)
    
### git branch -D <name> 强行删除一个还没有合并的分支
### 多人协作
- 查看远程库信息

  ```
  git remote
  git remote -v //更详细信息
  ```

- 推送分支

  ```
  git push origin master //远程库名字  分支也可以是dev
  ```

  *并不是一定要把本地分支远程推送*

  - master分支是主分支，因此要时刻与远程同步
  - dev分支是开发分支，团队所有成员需要在上面工作，所以也需要与远程同步
  - bug分支是用于本地修复bug,就没必要推送到远程了
  - feature分支是否推送远程，取决于你是否和你的小伙伴合作在上面开发

### git rebase

- 多人在同一个分支上协作时，很容易出现冲突。即使没有冲突，后push的童鞋不得不先pull，在本地合并，然后才能push成功。

  每次合并再push后，分支变成了这样：

  ````
  $ git log --graph --pretty=oneline --abbrev-commit
  * d1be385 (HEAD -> master, origin/master) init hello
  *   e5e69f1 Merge branch 'dev'
  |\  
  | *   57c53ab (origin/dev, dev) fix env conflict
  | |\  
  | | * 7a5e5dd add env
  | * | 7bd91f1 add new env
  | |/  
  * |   12a631b merged bug fix 101
  |\ \  
  | * | 4c805e2 fix bug 101
  |/ /  
  * |   e1e9c68 merge with no-ff
  |\ \  
  | |/  
  | * f52c633 add merge
  |/  
  *   cf810e4 conflict fixed
  ````

- 上面看上去很乱 ，从例子看，`hello.py`这个文件做了两次提交。用`git log`命令看看

  ```
  $ git log --graph --pretty=oneline --abbrev-commit
  * 582d922 (HEAD -> master) add author
  * 8875536 add comment
  * d1be385 (origin/master) init hello
  *   e5e69f1 Merge branch 'dev'
  |\  
  | *   57c53ab (origin/dev, dev) fix env conflict
  | |\  
  | | * 7a5e5dd add env
  | * | 7bd91f1 add new env
  ...
  ```

  *注意到Git用`(HEAD -> master)`和`(origin/master)`标识出当前分支的HEAD和远程origin的位置分别是`582d922 add author`和`d1be385 init hello`，本地分支比远程分支快两个提交。*

- 推送本地分支

  ```
  $ git push origin master
  To github.com:michaelliao/learngit.git
   ! [rejected]        master -> master (fetch first)
  error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
  hint: Updates were rejected because the remote contains work that you do
  hint: not have locally. This is usually caused by another repository pushing
  hint: to the same ref. You may want to first integrate the remote changes
  hint: (e.g., 'git pull ...') before pushing again.
  hint: See the 'Note about fast-forwards' in 'git push --help' for details.
  ```

- 这说明有人先于我们推送了远程分支。按照经验，先pull一下：

  ```
  $ git pull
  remote: Counting objects: 3, done.
  remote: Compressing objects: 100% (1/1), done.
  remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
  Unpacking objects: 100% (3/3), done.
  From github.com:michaelliao/learngit
     d1be385..f005ed4  master     -> origin/master
   * [new tag]         v1.0       -> v1.0
  Auto-merging hello.py
  Merge made by the 'recursive' strategy.
   hello.py | 1 +
   1 file changed, 1 insertion(+)
  ```

- 查看状态

  ```
  $ git status
  On branch master
  Your branch is ahead of 'origin/master' by 3 commits.
    (use "git push" to publish your local commits)
  
  nothing to commit, working tree clean
  ```

- 加上刚才合并的提交，现在我们本地分支比远程分支超前3个提交。

  ```
  $ git log --graph --pretty=oneline --abbrev-commit
  *   e0ea545 (HEAD -> master) Merge branch 'master' of github.com:michaelliao/learngit
  |\  
  | * f005ed4 (origin/master) set exit=1
  * | 582d922 add author
  * | 8875536 add comment
  |/  
  * d1be385 init hello
  ...
  ```

- 上面看起来很乱，我们使用命令整理成直线

  ```
  $ git rebase
  First, rewinding head to replay your work on top of it...
  Applying: add comment
  Using index info to reconstruct a base tree...
  M	hello.py
  Falling back to patching base and 3-way merge...
  Auto-merging hello.py
  Applying: add author
  Using index info to reconstruct a base tree...
  M	hello.py
  Falling back to patching base and 3-way merge...
  Auto-merging hello.py
  ```

  再查看

  ```
  $ git log --graph --pretty=oneline --abbrev-commit
  * 7e61ed4 (HEAD -> master) add author
  * 3611cfe add comment
  * f005ed4 (origin/master) set exit=1
  * d1be385 init hello
  ...
  ```

  其实原理非常简单。我们注意观察，发现Git把我们本地的提交“挪动”了位置，放到了`f005ed4 (origin/master) set exit=1`之后，这样，整个提交历史就成了一条直线。rebase操作前后，最终的提交内容是一致的，但是，我们本地的commit修改内容已经变化了，它们的修改不再基于`d1be385 init hello`，而是基于`f005ed4 (origin/master) set exit=1`，但最后的提交`7e61ed4`内容是一致的。

  rebase操作的特点：把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。

  最后，通过push操作把本地分支推送到远程：

  ```
  Mac:~/learngit michael$ git push origin master
  Counting objects: 6, done.
  Delta compression using up to 4 threads.
  Compressing objects: 100% (5/5), done.
  Writing objects: 100% (6/6), 576 bytes | 576.00 KiB/s, done.
  Total 6 (delta 2), reused 0 (delta 0)
  remote: Resolving deltas: 100% (2/2), completed with 1 local object.
  To github.com:michaelliao/learngit.git
     f005ed4..7e61ed4  master -> master
  ```

  再用`git log`看看效果：

  ```
  $ git log --graph --pretty=oneline --abbrev-commit
  * 7e61ed4 (HEAD -> master, origin/master) add author
  * 3611cfe add comment
  * f005ed4 set exit=1
  * d1be385 init hello
  ...
  ```

- 小结
  - rebase操作可以把本地未push的分叉提交历史整理成直线；
  - rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

## 标签

### 创建标签

- 切换到需要打标签的分支上，然后执行命令

  ```
  git tag v0.1
  ```

- 查看所有标签

  ```
  git tag
  ```

- 使用`git log`查看，找到历史提交的commit id 打标签

  ```
  git tag v0.1 f52dasf
  ```

- 查看标签信息

  ```
  git show v0.1
  ```

- 创建带有说明的标签

  ```
  git tag -a v0.1 -m "version 0.1" 1324324
  ```

  *-a 表示标签名 -m 表示说明*

- 注意：**标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。**

### 操作标签

- 删除标签

  ```
  git tag -d v0.1
  ```

- 推送标签到远程仓库

  ```
  git push origin v1.0
  ```

  或者一次性推送所有标签

  ```
  git push origin --tags
  ```

- 如果标签已经推送到远程，删除需要先删除本地，再删除远程

  ```
  git tag -d v0.1
  git push origin :refs/tags/v0.1
  ```

## 使用Github

- 在GitHub上，可以任意Fork开源仓库；

- 自己拥有Fork后的仓库的读写权限；

- 可以推送pull request给官方仓库来贡献代码

  
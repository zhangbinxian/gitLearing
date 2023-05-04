# git 



## download

``` 
https://git-scm.com/
```

## 启动

``` 
git bash
```

## 初始化git

``` 
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```



### 创建一个仓库(repository)

``` 
mkdir learngit
cd learngit
```



### 初始化管理仓库

``` 
git init

Initialized empty Git repository in /Users/michael/learngit/.git/

```

>
>
>瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个`.git`的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了 



## 创建一个新文件 readme.txt

```
内容
Git is a version control system.
Git is free software.
```

>
>
>### git add
>
>```
>git add 文件名
>添加文件到暂存区
>
>```
>
>### git commit -m 文件
>
>``` 
>git commit -m "本次提交的描述"
>提交到仓库
>
>```
>
>### git 可以一次提交多个文件
>
>```
>$ git add file1.txt
>$ git add file2.txt file3.txt
>$ git commit -m "add 3 files"
>
>```
>
>### git status
>
>```
>git status
>命令可以让我们时刻掌握仓库当前的状态
>
>```
>
>### git diff
>
>```
>git diff 文件名
>查看difference，显示的格式正是Unix通用的diff格式
>```
>
>###  git log
>
>```
>命令显示从最近到最远的提交日志
>
>commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
>Author: Michael Liao <askxuefeng@gmail.com>
>Date:   Fri May 18 21:06:15 2018 +0800
>
>append GPL
>
>commit e475afc93c209a690c39c13a46716e8fa000c366
>Author: Michael Liao <askxuefeng@gmail.com>
>Date:   Fri May 18 21:03:36 2018 +0800
>
>add distributed
>
>commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
>Author: Michael Liao <askxuefeng@gmail.com>
>Date:   Fri May 18 20:59:18 2018 +0800
>
>wrote a readme file
>
>```
>
>### git log --pretty=oneline(简洁输出log)
>
>```
>1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master) append GPL
>e475afc93c209a690c39c13a46716e8fa000c366 add distributed
>eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0 wrote a readme file
>
>commit id ==============================描述 
>
>head 表示当前版本
>```
>
>### 回滚 git reset --hard HEAD^
>
>```
>HEAD^表示上一个版本
>HEAD^^表示上上个版本
>
>或者
>HEAD~100 上100个版本
>
>```
>
>### 又回到当前刚刚上个版本
>
>```
>git reset --hard 版本id
>只要上面的命令窗口没有关闭，就可以找到log 和id
>
>id可以只写前几位 不用写全
>
>```
>
>```
>┌────┐
>│HEAD│
>└────┘
>│
>└──▶ ○ append GPL
>   │
>   ○ add distributed
>   │
>   ○ wrote a readme file
>   
>┌────┐
>│HEAD│
>└────┘
>│
>│    ○ append GPL
>│    │
>└──▶ ○ add distributed
>   │
>   ○ wrote a readme file
>
>```
>
>### git reflog
>
>```
>git reflog
>记录每一次命令
>```
>
>## 小结
>
>```
>HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
>
>穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
>
>要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
>```



# 工作区和暂存区

![ ![git-repo](https://www.liaoxuefeng.com/files/attachments/919020037470528/0) ]

第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支



`git add`命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支 

 一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的： 



![ ![git-stage-after-commit](https://www.liaoxuefeng.com/files/attachments/919020100829536/0) ]



##  Git跟踪并管理的是修改，而非文件 

 Git是如何跟踪修改的，每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中 



### git checkout -- 文件名

```
git checkout -- 文件名
工作区的修改全部撤销

一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态

```

###  git reset HEAD 文件名

```
git reset HEAD <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区

```

 `git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本 



场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD `，就回到了场景1，第二步按场景1操作。



```
1.没有git add时，用git checkout -- file

2.已经git add时，先git reset HEAD <file>回退到1.，再按1.操作

3.已经git commit时，用git reset回退版本

4.推送到远程库，GG?
```



### 删除文件

```
git rm 文件名

```

 现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit` 

 另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本 

```
git checkout -- 文件名

```



# git和github

>
>
>### 创建ssh key
>
>user/.ssh/id_rsa			私钥
>
>user/.ssh/id_rsa.pub	公钥
>
>
>
>如果没有以上文件的话
>
>#### 创建
>
>```
>ssh-keygen -t rsa -C "youremail@example.com"
>一路默认即可
>```
>
>#### github settings ssh key
>
>```
>添加刚刚复制的公钥
>
>```
>
>### 创建仓库 连接本地
>
>```
>git remote add origin git@github.com:自己的github地址/learngit.git
>远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库
>
>接下来会让你填写github username和password
>username	邮箱
>password	github的token
>```
>
>### push
>
>```
>git push -u origin master
>```
>
>加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令 
>
>
>
>从现在起，只要本地作了提交，就可以通过命令 
>
>```
>git push origin master
>
>```
>
>### 删除远程库
>
>```
>git remote rm origin
>
>```
>
>此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除 
>
>
>
>要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；
>
>关联一个远程库时必须给远程库指定一个名字，`origin`是默认习惯命名；
>
>关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；
>
>此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；
>
>###  
>
>### git clone
>
>```
>git clone 地址
>git clone https://github.com/zhangbinxian/gitLearing.git
>```



### 创建和合并分支

 在版本回退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即`master`分支。`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支 



 一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点 

```ascii
                  HEAD
                    │
                    │
                    ▼
                 master
                    │
                    │
                    ▼
┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘
```

 每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长 



 当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上 

```ascii
              master
                    │
                    │
                    ▼
┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘
                    ▲
                    │
                    │
                   dev
                    ▲
                    │
                    │
                  HEAD
```

 Git创建一个分支很快，因为除了增加一个`dev`指针，改改`HEAD`的指向，工作区的文件都没有任何变化！ 

 从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变 

```ascii
                master
                    │
                    │
                    ▼
┌───┐    ┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘    └───┘
                             ▲
                             │
                             │
                            dev
                             ▲
                             │
                             │
                           HEAD
```

 假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并 

```ascii
                           HEAD
                             │
                             │
                             ▼
                          master
                             │
                             │
                             ▼
┌───┐    ┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘    └───┘
                             ▲
                             │
                             │
                            dev
```

 所以Git合并分支也很快！就改改指针，工作区内容也不变 

合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支：

```ascii
                           HEAD
                             │
                             │
                             ▼
                          master
                             │
                             │
                             ▼
┌───┐    ┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘    └───┘
```



### 创建分支

>### 创建dev分支，切换到dev分支
>
>```
>git checkout -b dev
>
>Switched to a new branch 'dev'
>
>==============================================
>git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
>
>git branch dev
>git checkout dev
>
>Switched to branch 'dev'
>
>```
>
>### git branch 查看当前分支
>
>```
>git branch
>* dev
>master
>
>```
>
>然后，我们就可以在`dev`分支上正常提交，比如对`readme.txt`做个修改，加上一行：
>
>```
>Creating a new branch is quick.
>```
>
>添加 提交
>
>现在，`dev`分支的工作完成，我们就可以切换回`master`分支： 
>
>```
>git checkout master
>
>Switched to branch 'master'
>Your branch is up to date with 'origin/master'.
>```
>
>### git checkout dev或者master
>
>切换到相应的分支
>
>
>
>切换回`master`分支后，再查看一个`readme.txt`文件，刚才添加的内容不见了！因为那个提交是在`dev`分支上，而`master`分支此刻的提交点并没有变 
>
>![git-br-on-master](https://www.liaoxuefeng.com/files/attachments/919022533080576/0) 
>
>### git merge 合并分支
>
>```
>git merge dev
>
>Updating 2c1c01b..6d3a723
>Fast-forward	
>readme.txt | 3 ++-
>1 file changed, 2 insertions(+), 1 deletion(-)
>
>===========================================================
>Fast-forward Git告诉我们，这次合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快
>```
>
>合并后，再查看`readme.txt`的内容，就可以看到，和`dev`分支的最新提交是完全一样的 
>
>### 删除dev分支
>
>```
>git branch -d dev
>
>Deleted branch dev (was 6d3a723).
>```
>
>删除后，查看`branch`，就只剩下`master`分支了： 
>
>```
>git branch
>* master
>```
>
>### switch
>
>```
>git switch -c dev		创建并切换到新的branch
>
>git switch master		切换到以有的master分支
>
>
>```
>
>####  使用新的`git switch`命令，比`git checkout`要更容易理解 
>
>我们注意到切换分支使用`git checkout `，而前面讲过的撤销修改则是`git checkout -- `，同一个命令，有两种作用，确实有点令人迷惑。
>
>实际上，切换分支这个动作，用`switch`更科学。因此，最新版本的Git提供了新的`git switch`命令来切换分支：
>
>创建并切换到新的`dev`分支
>
>### 小结
>
>```
>Git鼓励大量使用分支：
>
>查看分支：git branch
>
>创建分支：git branch <name>
>
>切换分支：git checkout <name>或者git switch <name>
>
>创建+切换分支：git checkout -b <name>或者git switch -c <name>
>
>合并某分支到当前分支：git merge <name>
>
>删除分支：git branch -d <name>
>```
>
>
>
>###  准备新的`feature1`分支，继续我们的新分支开发
>
>```
>git switch -c feature1
>
>Switched to a new branch 'feature1'
>```
>
>修改`readme.txt`最后一行，改为：
>
>```
>Creating a new branch is quick AND simple.
>```
>
>在`feature1`分支上提交： 
>
>```
>git add readme.txt
>
>$ git commit -m "AND simple"
>[feature1 14096d0] AND simple
>1 file changed, 1 insertion(+), 1 deletion(-)
>```
>
>切换到`master`分支： 
>
>```
>Switched to branch 'master'
>D       python.py
>Your branch is ahead of 'origin/master' by 1 commit.
>(use "git push" to publish your local commits)
>
>Git还会自动提示我们当前master分支比远程的master分支要超前1个提交
>```
>
>在`master`分支上把`readme.txt`文件的最后一行改为：
>
>```
>Creating a new branch is quick & simple.
>```
>
>提交
>
>```
>git add readme.txt 
>git commit -m "& simple"
>[master 5dc6824] & simple
>1 file changed, 1 insertion(+), 1 deletion(-)
>```
>
>现在，`master`分支和`feature1`分支各自都分别有新的提交，变成了这样：
>
>```ascii
>                            HEAD
>                              │
>                              │
>                              ▼
>                           master
>                              │
>                              │
>                              ▼
>                            ┌───┐
>                         ┌─▶│   │
>┌───┐    ┌───┐    ┌───┐  │  └───┘
>│   │───▶│   │───▶│   │──┤
>└───┘    └───┘    └───┘  │  ┌───┐
>                         └─▶│   │
>                            └───┘
>                              ▲
>                              │
>                              │
>                          feature1
>```
>
>这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突 
>
>```
>git merge feature1
>Auto-merging readme.txt
>CONFLICT (content): Merge conflict in readme.txt
>Automatic merge failed; fix conflicts and then commit the result.
>```
>
>果然冲突了！Git告诉我们，`readme.txt`文件存在冲突，必须手动解决冲突后再提交。`git status`也可以告诉我们冲突的文件 
>
>我们可以直接查看readme.txt的内容 
>
>```
>Git is a distributed version control system.
>Git is free software distributed under the GPL.
>Git has a mutable index called stage.
>Git tracks changes
>five
>Creating a new branch is quick.
><<<<<<< HEAD
>Creating a new branch is quick & simple.
>=======
>Creating a new branch is quick AND simple.
>>>>>>>> featureal
>
>```
>
>Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，我们修改如下后保存 
>
>```
>Creating a new branch is quick and simple.
>```
>
>重新添加 提交
>
>现在，`master`分支和`feature1`分支变成了下图所示：
>
>```ascii
>                                     HEAD
>                                       │
>                                       │
>                                       ▼
>                                    master
>                                       │
>                                       │
>                                       ▼
>                            ┌───┐    ┌───┐
>                         ┌─▶│   │───▶│   │
>┌───┐    ┌───┐    ┌───┐  │  └───┘    └───┘
>│   │───▶│   │───▶│   │──┤             ▲
>└───┘    └───┘    └───┘  │  ┌───┐      │
>                         └─▶│   │──────┘
>                            └───┘
>                              ▲
>                              │
>                              │
>                          feature1
>```
>
>### git log --graph --pretty=oneline --abbrev-commit
>
>```
>*   1c84121 (HEAD -> master) conflict fixed
>|\
>| * 24c4d7b (featureal) and simple
>* | 565f5f6 simple
>|/
>* 6d3a723 branch
>* 2c1c01b (origin/master) markdown
>* 08d2f3c test
>* bf5bd25 new readme
>* a460134 new python
>* 2b0db0e LICENSE.txt
>* 2318754 remove test.txt
>* 79e8280 add test.txt
>* 902c02b git tracks changes
>* d0d67fb understand how stage works
>* 8433568 append GPL
>* c8a5b6a add distributed
>* fd11d29 wrote a readme file
>```
>
>最后，删除`feature1`分支： 
>
>```
>git branch -d featureal
>
>Deleted branch feature1 (was 14096d0).
>```
>
>### 小结
>
>```
>当Git无法自动合并分支时，就必须首先解决冲突,解决冲突后，再提交，合并完成。
>
>解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
>
>用`git log --graph`命令可以看到分支合并图
>
>```



### 分支管理策略

通常，合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息

下面我们实战一下`--no-ff`方式的`git merge` 

 

> 首先，仍然创建并切换`dev`分支 
>
> ```
> git switch -c dev
> Switched to a new branch 'dev'
> 
> ```
>
> 修改readme.txt文件，并提交一个新的commit： 
>
> ```
> git add readme.txt 
> git commit -m "add merge"
> <<<<<<< Updated upstream
> <<<<<<< Updated upstream
> =======
> >>>>>> Stashed changes
> 
> [dev f52c633] add merge
> 1 file changed, 1 insertion(+)
> 
> ```
>
> 现在，我们切换回`master`： 
>
> ```
> git switch master
> Switched to branch 'master'
> 
> ```
>
> 准备合并`dev`分支，请注意`--no-ff`参数，表示禁用`Fast forward`
>
> ```
> git merge --no-ff -m "merge with no-ff" dev
> Merge made by the 'recursive' strategy.
> readme.txt | 1 +
> 1 file changed, 1 insertion(+)
> 
> ```
>
> 因为本次合并要创建一个新的commit，所以加上`-m`参数，把commit描述写进去 
>
> 合并后，我们用`git log`看看分支历史 
>
> ```
> git log --graph --pretty=oneline --abbrev-commit
> 
> *   3c60a75 (HEAD -> master) merge with no--ff
>  |\
>  | * 0d2bd4d (dev) add merge
>  |/
> *   46b7672 (origin/master) markdown
> *   a8a8091 git.md
> *   8323125 new markdown
> *   1c84121 conflict fixed
>  |\
>  | * 24c4d7b and simple
> *   | 565f5f6 simple
>  |/
> *   6d3a723 branch
> *   2c1c01b markdown
> *   08d2f3c test
> *   bf5bd25 new readme
> *   a460134 new python
> *   2b0db0e LICENSE.txt
> *   2318754 remove test.txt
> *   79e8280 add test.txt
> *   902c02b git tracks changes
> *   d0d67fb understand how stage works
> *   8433568 append GPL
> *   c8a5b6a add distributed
> *   fd11d29 wrote a readme file
> 
> ```
>
> 可以看到，不使用`Fast forward`模式，merge后就像这样：
>
> ![git-no-ff-mode](https://www.liaoxuefeng.com/files/attachments/919023225142304/0)
>
> ### 分支策略
>
> 在实际开发中，我们应该按照几个基本原则进行分支管理：
>
> 首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
>
> 那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；
>
> 你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了
>
> 所以，团队合作的分支看起来就像这样：
>
> ![git-br-policy](https://www.liaoxuefeng.com/files/attachments/919023260793600/0)
>
> 合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并 

### BUG分支

> 软件开发中，bug就像家常便饭一样。有了bug就需要修复，在Git中，由于分支是如此的强大，所以，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除 
>
> 当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支`issue-101`来修复它，但是，等等，当前正在`dev`上进行的工作还没有提交 
>
> ```
> $ git status
> On branch dev
> Changes to be committed:
> (use "git reset HEAD <file>..." to unstage)
> 
> 	new file:   hello.py
> 
> Changes not staged for commit:
> (use "git add <file>..." to update what will be committed)
> (use "git checkout -- <file>..." to discard changes in working directory)
> 
> 	modified:   readme.txt
> 	
> ```
>
> 并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？
>
> 幸好，Git还提供了一个`stash`功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：
>
> ```
> git stash
> Saved working directory and index state WIP on dev: f52c633 add merge
> ```
>
> 首先确定要在哪个分支上修复bug，假定需要在`master`分支上修复，就从`master`创建临时分支 
>
> ```
> git checkout master
> Switched to branch 'master'
> Your branch is ahead of 'origin/master' by 6 commits.
> (use "git push" to publish your local commits)
> 
> $ git checkout -b issue-101
> Switched to a new branch 'issue-101'
> 
> ```
>
> 现在修复bug，需要把“Git is free software ...”改为“Git is a free software ... ,提交
>
> ```
> git add readme.txt 
> git commit -m "fix bug 101"
> [issue-101 4c805e2] fix bug 101
> 1 file changed, 1 insertion(+), 1 deletion(-)
> 
> ```
>
> 修复完成后，切换到`master`分支，并完成合并，最后删除`issue-101`分支 
>
> ```
> git switch master
> Switched to branch 'master'
> Your branch is ahead of 'origin/master' by 6 commits.
> (use "git push" to publish your local commits)
> 
> git merge --no-ff -m "merged bug fix 101" issue-101
> Merge made by the 'recursive' strategy.
> readme.txt | 2 +-
> 1 file changed, 1 insertion(+), 1 deletion(-)
> ```
>
> 太棒了，原计划两个小时的bug修复只花了5分钟！现在，是时候接着回到`dev`分支干活了！ 
>
> ```
> $ git switch dev
> Switched to branch 'dev'
> 
> $ git status
> On branch dev
> nothing to commit, working tree clean
> 
> 
> ```
>
> 工作区是干净的，刚才的工作现场存到哪去了？用`git stash list`命令看看 
>
> ```
> git stash list
> 
> stash@{0}: WIP on master: 3c60a75 merge with no--ff
> 
> ```
>
> 工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
>
> 一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；
>
> 
>
> 另一种方式是用`git stash pop`，恢复的同时把stash内容也删了： 
>
> ```
> git stash pop
> On branch dev
> Changes to be committed:
> (use "git reset HEAD <file>..." to unstage)
> 
> 	new file:   hello.py
> 
> Changes not staged for commit:
> (use "git add <file>..." to update what will be committed)
> (use "git checkout -- <file>..." to discard changes in working directory)
> 
> 	modified:   readme.txt
> 
> Dropped refs/stash@{0} (5d677e2ee266f39ea296182fb2354265b91b3b2a)
> ```
>
> 再用`git stash list`查看，就看不到任何stash内容了 
>
> ```
> git stash list
> 
> ```
>
> 你可以多次stash，恢复的时候，先用`git stash list`查看，然后恢复指定的stash，用命令： 
>
> ```
> git stash apply stash@{0}
> 
> 
> ```
>
> 在master分支上修复了bug后，我们要想一想，dev分支是早期从master分支分出来的，所以，这个bug其实在当前dev分支上也存在。
>
> 那怎么在dev分支上修复同样的bug？重复操作一次，提交不就行了？
>
> 有木有更简单的方法？
>
> 有！
>
> 
>
> 同样的bug，要在dev上修复，我们只需要把`4c805e2 fix bug 101`这个提交所做的修改“复制”到dev分支。注意：我们只想复制`4c805e2 fix bug 101`这个提交所做的修改，并不是把整个master分支merge过来。
>
> 为了方便操作，Git专门提供了一个`cherry-pick`命令，让我们能复制一个特定的提交到当前分支：
>
> ```
> 
> ```
>
> Git自动给dev分支做了一次提交，注意这次提交的commit是`1d4b803`，它并不同于master的`4c805e2`，因为这两个commit只是改动相同，但确实是两个不同的commit。用`git cherry-pick`，我们就不需要在dev分支上手动再把修bug的过程重复一遍。 
>
> 
>
> ### 小结
>
> 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
>
> 当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；
>
> 在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick `命令，把bug提交的修改“复制”到当前分支，避免重复劳动

### Feature分支

>
>
>软件开发中，总有无穷无尽的新的功能要不断添加进来。
>
>添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。
>
>现在，你终于接到了一个新任务：开发代号为Vulcan的新功能，该功能计划用于下一代星际飞船。
>
>#### 得到一个新任务
>
>准备开发
>
>```
>git switch -c feature-vulcan
>Switched to a new branch 'feature-vulcan'
>
>```
>
>一段时间后，开发完毕，添加，commit
>
>```
>git add vulcan.py
>
>git status
>On branch feature-vulacn
>Changes to be committed:
>(use "git restore --staged <file>..." to unstage)
>   new file:   vulcan.py
>   
>git commit -m "add vulcan.py"
>[feature-vulacn e6952dd] add vulcan.py
>1 file changed, 1 insertion(+)
>create mode 100644 vulcan.py
>
>```
>
>切回`dev`，准备合并： 
>
>```
>git switch dev
>```
>
>一切顺利的话，feature分支和bug分支是类似的，合并，然后删除。
>
>但是！
>
>
>
>就在此时，接到上级命令，因经费不足，新功能必须取消！
>
>虽然白干了，但是这个包含机密资料的分支还是必须就地销毁：
>
>```
>git branch -d feature-vulacn
>
>error: The branch 'feature-vulacn' is not fully merged.
>If you are sure you want to delete it, run 'git branch -D feature-vulacn'.
>
>
>```
>
>销毁失败。Git友情提醒，`feature-vulcan`分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用大写的`-D`参数。 
>
>
>
>现在，我们强行删除
>
>```
>git branch -D feature-vulacn
>Deleted branch feature-vulacn (was e6952dd).
>
>```
>
>ok啦，删除成功
>
>### 小结
>
>开发一个新feature，最好新建一个分支；
>
>如果要丢弃一个没有被合并过的分支，可以通过`git branch -D `强行删除。



### 多人协同

>当你从远程仓库克隆时，实际上Git自动把本地的`master`分支和远程的`master`分支对应起来了，并且，远程仓库的默认名称是`origin`。
>
>要查看远程库的信息，用`git remote`：
>
>```
>git remote
>origin
>```
>
>或者，用`git remote -v`显示更详细的信息 
>
>```
>git remote -v
>
>origin  https://github.com/zhangbinxian/gitLearing.git (fetch)
>origin  https://github.com/zhangbinxian/gitLearing.git (push)
>```
>
>上面显示了可以抓取和推送的`origin`的地址。如果没有推送权限，就看不到push的地址。 
>
>
>
>### 推送分支
>
>推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上 
>
>```
>git push origin master
>
>```
>
>如果要推送其他分支，比如`dev`，就改成 
>
>```
>gti push origin dev
>
>```
>
>但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢 
>
>```
>master分支是主分支，因此要时刻与远程同步；
>
>dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
>
>bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
>
>feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发
>
>
>```
>
>### 抓取分支
>
>多人协作时，大家都会往`master`和`dev`分支上推送各自的修改 
>
>模拟一个你的小伙伴，可以在另一台电脑（注意要把SSH Key添加到GitHub）或者同一台电脑的另一个目录下克隆 
>
>```
>git clone https://github.com/zhangbinxian/gitLearing.git
>Cloning into 'gitLearing'...
>remote: Enumerating objects: 89, done.
>remote: Counting objects: 100% (89/89), done.
>remote: Compressing objects: 100% (52/52), done.
>Receiving objects:  64% (57/89)used 76 (delta 27), pack-reused 0Receiving objects:  49% (44/89)
>Receiving objects: 100% (89/89), 18.70 KiB | 6.23 MiB/s, done.
>Resolving deltas: 100% (37/37), done.
>
>```
>
>当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的`master`分支。不信可以用`git branch`命令看看 
>
>```
>git branch
>*main
>
>```
>
>现在，你的小伙伴要在`dev`分支上开发，就必须创建远程`origin`的`dev`分支到本地，于是他用这个命令创建本地`dev`分支 
>
>```
>git checkout -b origin/dev
>
>
>```
>
>现在，他就可以在`dev`上继续修改，然后，时不时地把`dev`分支`push`到远程 
>
>```
>$ git add env.txt
>
>$ git commit -m "add env"
>[dev 7a5e5dd] add env
>1 file changed, 1 insertion(+)
>create mode 100644 env.txt
>
>$ git push origin dev
>Counting objects: 3, done.
>Delta compression using up to 4 threads.
>Compressing objects: 100% (2/2), done.
>Writing objects: 100% (3/3), 308 bytes | 308.00 KiB/s, done.
>Total 3 (delta 0), reused 0 (delta 0)
>To github.com:michaelliao/learngit.git
>f52c633..7a5e5dd  dev -> dev
>
>
>```
>
>你的小伙伴已经向`origin/dev`分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送 
>
>```
>$ cat env.txt
>env
>
>$ git add env.txt
>
>$ git commit -m "add new env"
>[dev 7bd91f1] add new env
>1 file changed, 1 insertion(+)
>create mode 100644 env.txt
>
>$ git push origin dev
>To github.com:michaelliao/learngit.git
>! [rejected]        dev -> dev (non-fast-forward)
>error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
>hint: Updates were rejected because the tip of your current branch is behind
>hint: its remote counterpart. Integrate the remote changes (e.g.
>hint: 'git pull ...') before pushing again.
>hint: See the 'Note about fast-forwards' in 'git push --help' for details.
>
>
>```
>
>推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用`git pull`把最新的提交从`origin/dev`抓下来，然后，在本地合并，解决冲突，再推送 
>
>```
>git pull
>There is no tracking information for the current branch.
>Please specify which branch you want to merge with.
>See git-pull(1) for details.
>
>git pull <remote> <branch>
>
>If you wish to set tracking information for this branch you can do so with:
>
>git branch --set-upstream-to=origin/<branch> dev
>
>```
>
>`git pull`也失败了，原因是没有指定本地`dev`分支与远程`origin/dev`分支的链接，根据提示，设置`dev`和`origin/dev`的链接 
>
>```
>$ git branch --set-upstream-to=origin/dev dev
>Branch 'dev' set up to track remote branch 'dev' from 'origin'
>
>```
>
>再pull
>
>这回`git pull`成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的[解决冲突](http://www.liaoxuefeng.com/wiki/896043488029600/900004111093344)完全一样。解决后，提交，再push 
>
>### 小结
>
>多人协作的工作模式通常是这样：
>
>1. 首先，可以试图用`git push origin `推送自己的修改；
>
>2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
>
>3. 如果合并有冲突，则解决冲突，并在本地提交；
>
>4. 没有冲突或者解决掉冲突后，再用`git push origin `推送就能成功！
>
>5. 如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to  origin/`。
>
>这就是多人协作的工作模式，一旦熟悉了，就非常简单
>
>
>
>查看远程库信息，使用`git remote -v`；
>
>本地新建的分支如果不推送到远程，对其他人就是不可见的；
>
>从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
>
>在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
>
>建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
>
>从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突

### rebase

>
>
>在上一节我们看到了，多人在同一个分支上协作时，很容易出现冲突。即使没有冲突，后push的童鞋不得不先pull，在本地合并，然后才能push成功。
>
>每次合并再push后，分支变成了这样
>
>```
>$ git log --graph --pretty=oneline --abbrev-commit
>* d1be385 (HEAD -> master, origin/master) init hello
>*   e5e69f1 Merge branch 'dev'
>|\  
>| *   57c53ab (origin/dev, dev) fix env conflict
>| |\  
>| | * 7a5e5dd add env
>| * | 7bd91f1 add new env
>| |/  
>* |   12a631b merged bug fix 101
>|\ \  
>| * | 4c805e2 fix bug 101
>|/ /  
>* |   e1e9c68 merge with no-ff
>|\ \  
>| |/  
>| * f52c633 add merge
>|/  
>*   cf810e4 conflict fixed
>
>```
>
>总之看上去很乱，有强迫症的童鞋会问：为什么Git的提交历史不能是一条干净的直线？
>
>其实是可以做到的！
>
>Git有一种称为rebase的操作，有人把它翻译成“变基”
>
>
>
>在和远程分支同步后，我们对`hello.py`这个文件做了两次提交。用`git log`命令看看 
>
>```
>$ git log --graph --pretty=oneline --abbrev-commit
>* 582d922 (HEAD -> master) add author
>* 8875536 add comment
>* d1be385 (origin/master) init hello
>*   e5e69f1 Merge branch 'dev'
>|\  
>| *   57c53ab (origin/dev, dev) fix env conflict
>| |\  
>| | * 7a5e5dd add env
>| * | 7bd91f1 add new env
>...
>
>
>```
>
>注意到Git用`(HEAD -> master)`和`(origin/master)`标识出当前分支的HEAD和远程origin的位置分别是`582d922 add author`和`d1be385 init hello`，本地分支比远程分支快两个提交。
>
>现在我们尝试推送本地分支
>
>```
>$ git push origin master
>To github.com:michaelliao/learngit.git
>! [rejected]        master -> master (fetch first)
>error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
>hint: Updates were rejected because the remote contains work that you do
>hint: not have locally. This is usually caused by another repository pushing
>hint: to the same ref. You may want to first integrate the remote changes
>hint: (e.g., 'git pull ...') before pushing again.
>hint: See the 'Note about fast-forwards' in 'git push --help' for details
>
>
>```
>
>很不幸，失败了，这说明有人先于我们推送了远程分支。按照经验，先pull一下 
>
>```
>$ git pull
>remote: Counting objects: 3, done.
>remote: Compressing objects: 100% (1/1), done.
>remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
>Unpacking objects: 100% (3/3), done.
>From github.com:michaelliao/learngit
>d1be385..f005ed4  master     -> origin/master
>* [new tag]         v1.0       -> v1.0
>Auto-merging hello.py
>Merge made by the 'recursive' strategy.
>hello.py | 1 +
>1 file changed, 1 insertion(+)
>
>
>```
>
>再用git status
>
>```
>$ git status
>On branch master
>Your branch is ahead of 'origin/master' by 3 commits.
>(use "git push" to publish your local commits)
>
>nothing to commit, working tree clean
>
>```
>
>加上刚才合并的提交，现在我们本地分支比远程分支超前3个提交。
>
>用`git log`看看
>
>```
>$ git log --graph --pretty=oneline --abbrev-commit
>*   e0ea545 (HEAD -> master) Merge branch 'master' of github.com:michaelliao/learngit
>|\  
>| * f005ed4 (origin/master) set exit=1
>* | 582d922 add author
>* | 8875536 add comment
>|/  
>* d1be385 init hello
>
>
>```
>
>对强迫症童鞋来说，现在事情有点不对头，提交历史分叉了。如果现在把本地分支push到远程，有没有问题？
>
>有！
>
>什么问题？
>
>不好看！
>
>有没有解决方法？
>
>有！
>
>这个时候，rebase就派上了用场。我们输入命令`git rebase`试试
>
>```
>$ git rebase
>First, rewinding head to replay your work on top of it...
>Applying: add comment
>Using index info to reconstruct a base tree...
>M	hello.py
>Falling back to patching base and 3-way merge...
>Auto-merging hello.py
>Applying: add author
>Using index info to reconstruct a base tree...
>M	hello.py
>Falling back to patching base and 3-way merge...
>Auto-merging hello.py
>
>
>```
>
>输出了一大堆操作，到底是啥效果？再用`git log`看看 
>
>```
>git log --graph --pretty=oneline --abbrev-commit
>* 7e61ed4 (HEAD -> master) add author
>* 3611cfe add comment
>* f005ed4 (origin/master) set exit=1
>* d1be385 init hello
>
>```
>
>原本分叉的提交现在变成一条直线了！这种神奇的操作是怎么实现的？其实原理非常简单。我们注意观察，发现Git把我们本地的提交“挪动”了位置，放到了`f005ed4 (origin/master) set exit=1`之后，这样，整个提交历史就成了一条直线。rebase操作前后，最终的提交内容是一致的，但是，我们本地的commit修改内容已经变化了，它们的修改不再基于`d1be385 init hello`，而是基于`f005ed4 (origin/master) set exit=1`，但最后的提交`7e61ed4`内容是一致的。
>
>这就是rebase操作的特点：把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。
>
>最后，通过push操作把本地分支推送到远程
>
>```
>git push origin master
>Counting objects: 6, done.
>Delta compression using up to 4 threads.
>Compressing objects: 100% (5/5), done.
>Writing objects: 100% (6/6), 576 bytes | 576.00 KiB/s, done.
>Total 6 (delta 2), reused 0 (delta 0)
>remote: Resolving deltas: 100% (2/2), completed with 1 local object.
>To github.com:michaelliao/learngit.git
>f005ed4..7e61ed4  master -> master
>
>```
>
>再用`git log`看看效果 
>
>```
>git log --graph --pretty=oneline --abbrev-commit
>* 7e61ed4 (HEAD -> master, origin/master) add author
>* 3611cfe add comment
>* f005ed4 set exit=1
>* d1be385 init hello
>
>
>```
>
>远程分支的提交历史也是一条直线 
>
>### 小结
>
>- rebase操作可以把本地未push的分叉提交历史整理成直线；
>- rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比

### 标签管理

>发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。
>
>Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。
>
>Git有commit，为什么还要引入tag？
>
>“请把上周一的那个版本打包发布，commit号是6a5819e...”
>
>“一串乱七八糟的数字不好找！”
>
>如果换一个办法：
>
>“请把上周一的那个版本打包发布，版本号是v1.2”
>
>“好的，按照tag v1.2查找commit就行！”
>
>所以，tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起
>
>
>
>### 创建标签
>
>在Git中打标签非常简单，首先，切换到需要打标签的分支上 
>
>```
>$ git branch
>* dev
>master
>$ git checkout master
>Switched to branch 'master'
>
>
>```
>
>```
>$ git tag v1.0
>
>
>```
>
>可以用命令`git tag`查看所有标签 
>
>```
>$ git tag
>v1.0
>
>
>```
>
>默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？
>
>方法是找到历史提交的commit id，然后打上就可以了
>
>```
>$ git log --pretty=oneline --abbrev-commit
>12a631b (HEAD -> master, tag: v1.0, origin/master) merged bug fix 101
>4c805e2 fix bug 101
>e1e9c68 merge with no-ff
>f52c633 add merge
>cf810e4 conflict fixed
>5dc6824 & simple
>14096d0 AND simple
>b17d20e branch test
>d46f35e remove test.txt
>b84166e add test.txt
>519219b git tracks changes
>e43a48b understand how stage works
>1094adb append GPL
>e475afc add distributed
>eaadf4e wrote a readme file
>
>
>```
>
>比方说要对`add merge`这次提交打标签，它对应的commit id是`f52c633`，敲入命令 
>
>```
>git tag v0.9 f52c633
>
>
>```
>
>再用命令`git tag`查看标签： 
>
>```
>$ git tag
>v0.9
>v1.0
>
>
>```
>
>注意，标签不是按时间顺序列出，而是按字母排序的。可以用`git show `查看标签信息：
>
>```
>$ git show v0.9
>commit f52c63349bc3c1593499807e5c8e972b82c8f286 (tag: v0.9)
>Author: Michael Liao <askxuefeng@gmail.com>
>Date:   Fri May 18 21:56:54 2018 +0800
>
>add merge
>
>diff --git a/readme.txt b/readme.txt
>
>```
>
>可以看到，`v0.9`确实打在`add merge`这次提交上。
>
>还可以创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字：
>
>```
>$ git tag -a v0.1 -m "version 0.1 released" 1094adb
>
>
>```
>
>用命令`git show `可以看到说明文字：
>
>```
>$ git show v0.1
>tag v0.1
>Tagger: Michael Liao <askxuefeng@gmail.com>
>Date:   Fri May 18 22:48:43 2018 +0800
>
>version 0.1 released
>
>commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (tag: v0.1)
>Author: Michael Liao <askxuefeng@gmail.com>
>Date:   Fri May 18 21:06:15 2018 +0800
>
>append GPL
>
>diff --git a/readme.txt b/readme.txt
>...
>
>```
>
>### 小结
>
>命令`git tag `用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
>
>命令`git tag -a  -m "blablabla..."`可以指定标签信息；
>
>命令`git tag`可以查看所有标签
>
>### 操作标签
>
>如果标签打错了，也可以删除：
>
>```
>$ git tag -d v0.1
>Deleted tag 'v0.1' (was f15b0dd)
>
>```
>
>因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除
>
>如果要推送某个标签到远程，使用命令`git push origin `：
>
>```
>$ git push origin v1.0
>Total 0 (delta 0), reused 0 (delta 0)
>To github.com:michaelliao/learngit.git
>* [new tag]         v1.0 -> v1.0
>
>```
>
>或者，一次性推送全部尚未推送到远程的本地标签：
>
>```
>$ git push origin --tags
>Total 0 (delta 0), reused 0 (delta 0)
>To github.com:michaelliao/learngit.git
>* [new tag]         v0.9 -> v0.9
>
>```
>
>如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
>
>```
>$ git tag -d v0.9
>Deleted tag 'v0.9' (was f52c633)
>
>```
>
>然后，从远程删除。删除命令也是push，但是格式如下：
>
>```
>$ git push origin :refs/tags/v0.9
>To github.com:michaelliao/learngit.git
>- [deleted]         v0.9
>
>
>```
>
>### 小结
>
>命令`git push origin `可以推送一个本地标签；
>
>命令`git push origin --tags`可以推送全部未推送过的本地标签；
>
>命令`git tag -d `可以删除一个本地标签；
>
>命令`git push origin :refs/tags/`可以删除一个远程标签












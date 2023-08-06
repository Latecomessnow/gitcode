# Git版本控制器

## 1. git安装与卸载

- **查看是否已经安装了git及其版本号**

  ```shell
  git --version
  ```

- **安装**:

  ```shell
  sudo yum install git -y
  ```

- **卸载**

  ```shell
  sudo yum remove git -y
  ```

## 2. 创建仓库并初始化

 - **创建需要进行版本控制的仓库**

   ```shell
   mkdir newRepository
   ```

- **进入仓库**

  ```shell
  cd newRepository
  ```

- **初始化仓库**

  ```shell
  git init
  ```

  初始化完仓库后就可以看到仓库中创建好的 `.git` 目录，用于版本管理，不可手动去修改文件内容，否则会造成无法正常进行版本管理的后果  。

  执行 `tree .git/` 命令可看到如下内容: 

  ![image-20230803110550160](C:\Users\Librocit\AppData\Roaming\Typora\typora-user-images\image-20230803110550160.png)

## 3. 配置git的用户名和邮箱

 - **查看 `git`的配置情况**

   ```shell
   git config -l
   ```

- **配置用户名**

  ```shell
  git config user.name "guhui"
  ```

- **配置邮箱**

  ```shell
  git config user.email "hui.yumhappy@gmail.com"
  ```

- **删除用户名**

  ```shell
  git config --unset user.name
  ```

- **删除邮箱**

  ```shell
  git config --unset user.email
  ```

- **配置全局的用户名(在所有 `git` 仓库中都有效的用户名)**

  ```shell
  git config --global user.name "guhui"
  ```

- **配置全局的邮箱(在所有 `git` 仓库中都有效的邮箱)**

  ```shell
  git config --global user.email "hui.yumhappy@gmail.com"
  ```

- **删除全局的用户名**

  ```shell
  git config --global --unset user.name
  ```

- **删除全局的邮箱**

  ```shell
  git config --global --unset user.email
  ```

## 4. 初识工作区、暂存区和版本库

- **工作区**

  就是使用 `mkdir` 命令创建出来的目录，当然好需要使用 `git init` 初始化一下，是在电脑上你要写代码或⽂件的⽬录，但不包括其目录下的 `.git/` 目录。

- **版本库**

  ⼜名仓库，英⽂名 `repository` 。⼯作区有⼀个隐藏⽬录  `.git` ，它不算⼯作区，⽽ 是 Git 的版本库，版本库中存在暂存区和分支。这个版本库⾥⾯的所有⽂件都可以被 Git 管理起来，每个⽂件的修改、删除，Git 都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

- **暂存区**

  英⽂叫 `stage `或 `index`。⼀般存放在 .git ⽬录下的 index ⽂件（.git/index）中，我们 把暂存区有时也叫作索引（index）。

## 5. git基本操作

- **添加文件至暂存区**

  ```shell
  git add README.md # 添加指定已修改的文件
  ```

  ```shell
  git add . # 添加工作区中所有已修改的文件
  ```

- **把暂存区的文件添加到本地仓库中(只有提交到本地仓库中的文件才能进行版本管理)**

  ```shell
  git commit -m "记录提交本次文件所作的修改日志" # 日志方便后边的查看
  ```

- **查看git的提交日志**

  ```shell
  git log
  ```

- **按行打印git提交日志**

  ```shell
  git log --pretty=on
  ```

- **认识`commit id`**

  每次进行`git commit`命令时都会有一个`commit id`，`commit id`的可以通过查看提交日志获取，或者在`.git/`目录下查看，如下

  ![image-20230803161249532](C:\Users\Librocit\AppData\Roaming\Typora\typora-user-images\image-20230803161249532.png)

- **查看某次commit所做的修改**

  ```shelll
  git cat-file -p [commit id]
  ```

  ![image-20230803161415887](C:\Users\Librocit\AppData\Roaming\Typora\typora-user-images\image-20230803161415887.png)

- **查看上次提交之后是否对文件进行修改**

  ```shlel
  git status
  ```

- **显示暂存区和⼯作区⽂件的差异**

  ```shell
  git diff [file]
  ```

  

## 6. git版本回退(重要操作)

回退选项:

> `--hard`: 参数将暂存区与⼯作区都退回到指定版本。切记⼯作区有未提交的代码时不要⽤这个命令，因为⼯作区会回滚，你没有提交的代码就再也找不回了，所以使⽤该参数前⼀定要慎重。
>
> `--mixed`: 回退到暂存区(不带参数默认也是回退到暂存区)，该参数将暂存区的内容退回为指定提交版本内 容，⼯作区⽂件保持不变。
>
> `--soft`: 于⼯作区和暂存区的内容都不变，只是将版本库回退到某个指定版本

- **回退命令**

  可先使用`git log --pretty=oneline`命令查看`commit id`

  ```shell
  git reset --hard [commit id]
  ```

  操作结果如下: 

  ![image-20230803231138333](C:\Users\Librocit\AppData\Roaming\Typora\typora-user-images\image-20230803231138333.png)



- **查看每一次的历史提交命令(可查看每一次的commit id)**

  ```shell
  git reflog
  ```

  例如将经过回退后，回退到指定`commit id`之后的操作就没了，如果想回退到`commit id`之后的位置可采用此命令  

  如如下操作所示: 

  ![image-20230805093154151](C:\Users\Librocit\AppData\Roaming\Typora\typora-user-images\image-20230805093154151.png)

- **撤销工作区新增的内容，但并未进行`git add`操作，可使用该命令回退**

  ```shell
  git checkout -- [filename]
  ```

  操作结果如下:

  ![image-20230805095341781](C:\Users\Librocit\AppData\Roaming\Typora\typora-user-images\image-20230805095341781.png)

- **将工作区和暂存区回退到当前版本库的内容**

  ```shell
  git reset HEAD [filename]   # 回退到当前版本 
  git reset HEAD^ [filename]  # 回退到上一个版本
  git reset HEAD^^ [filename] # 回退到上上一个版本
  ```

- **删除工作区和暂存区的某个文件**

  ```shell
  git rm [filename]
  ```

   

## 7. git分支管理

- **查看当前仓库素所存在的分支(有`*`号的分支表示当前工作区所处的分支)**

  ```shell
  git branch
  ```

- **创建新的分支**

  ```shell
  git branch [yourbranch]
  ```

- **切换分支**

  切换分支后，对工作区文件所作的任何修改都不会影响到其他分支，除非其他分支合并了该分支，该分支所做的修改才会体现上其他分支上

  ```shell
  git checkout [yourbranch]
  ```

- **在当前分支下合并其他分支**

  ```shell
  git merge [otherbranch]
  ```

- **删除分支(将其他分支合并到`master`主分支就可以考虑删除其他分支了)**

  ```shell
  git branch -d [yourbranch]
  ```

  住: 不能在使用某个分支下，然后去删除该分支，一般需要去切换到`master`分支去删除其他分支

- **切换到未创建的新分支上命令**

  ```shell
  git checkout -b [newBranchName]
  ```

- **板寸分支信息的合并(删除该分支后仍能看到该分支的commit信息)**

  ```shell
  git merge --no-ff -m"xxx" [yourbranch]
  ```

- **强制删除分支**

  新创建的分支，开发好之后合并到主分支上，合并完之后可以采用`git branch -d [yourBranch]`命令删除该分支，但是如果你需要删除未合并到主分支上的分支，``git branch -d`命令就不适用了。

  ```shell
  git branch -D [yourBranch]
  ```

## 8. git远程操作

首先需要在`github`或者`gitee`平台上根据提示创建远程的仓库，远程仓库名默认为`origin`，创建好远程仓库后，就可以和本地仓库进行交互了，例如，可以将本地仓库上的代码、文件、项目...推送至`github`远程仓库上，这样就可以很方便随时随地的查看你的代码了，当然了这样做的好处是更有助于多人进行协同开发，同样也可以将远程仓库中的内容拉取到本地仓库中。

- **克隆远程仓库到本地**

  ```shell
  git clone [远程仓库的地址]
  ```

  操作结果如下: 

  1. 查看远程仓库的地址

     ![image-20230806152619227](C:\Users\Librocit\AppData\Roaming\Typora\typora-user-images\image-20230806152619227.png)

  2. 使用`git clone`命令克隆仓库

     ![image-20230806152730693](C:\Users\Librocit\AppData\Roaming\Typora\typora-user-images\image-20230806152730693.png)

  3. 使用`git remote -v`命令查看远程仓库的详细信息

     

- **查看比较简洁的日志**

  ```shell
  git log --pretty=oneline --abbrev-commit 
  ```

- **给较长的命令取别名**

  如给`git log --pretty=oneline --abbrev-commit `起别名成`git ll`

  ```shell
  git config --global alias.ll 'log --pretty=oneline --abbrev-commit'
  ```

  ![image-20230806201321098](C:\Users\Librocit\AppData\Roaming\Typora\typora-user-images\image-20230806201321098.png)

  类似的也可以给`git status`起别名成`git st`

  ```shell
  git config --global alias.st status
  ```

- **查看当前`git`存在的标签**

  ```shell
  git tag
  ```

- **给某一次提交的版本打标签**

  ```shell
  git tag [tag name] [commit id]
  ```

  如给第一次提交的版本打一个标签`v1.0`

  ![image-20230806201807625](C:\Users\Librocit\AppData\Roaming\Typora\typora-user-images\image-20230806201807625.png)

- **查看某个标签的具体内容**

  ```shell
  git show [tag name]
  ```

- **删除标签**

  ```shell
  git tag -d [tag name]
  ```

  

  

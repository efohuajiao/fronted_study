# Git学习

git是免费、开源的**分布式版本控制工具**，可以快速高效地处理从小型到大型地各种项目。

## github

- 代码推送 push
- 代码拉取 pull
- 代码克隆 clone
- SSH免密登录

## 版本控制

版本控制就是一种**记录文件内容变化**、以便将来查阅特定版本修订情况的系统。

版本控制最重要的是可以记录文件修改历史记录，从而让用户能够查看历史版本，方便版本切换。

##  代码托管中心

代码托管中心是基于网络服务器的远程代码仓库，一般简单成为**远程库**

- 局域网
  - GitLab
- 互联网
  - GitHub（外网）
  - Gitee码云（国内）

## Git常用命令

| 命令名称                                           | 作用               |
| -------------------------------------------------- | ------------------ |
| git config --global user.name 用户名               | 设置用户签名       |
| git config --global user.email 邮箱                | 设置用户邮箱       |
| git init                                           | 初始化本地库       |
| git status                                         | 查看本地库状态     |
| git add 文件名(git add . 添加当前目录下的所有文件) | 将文件添加到暂存区 |
| git commit -m "日志信息" 文件名                    | 提交到本地库       |
| git reflog                                         | 查看历史记录       |
| git reset --hard 版本号                            | 版本穿梭           |

### 设置用户签名和邮箱

`git config --global user.name efohuajiao`

`git config --global user.email 3080680474@qq.com`

签名的作用是区分不同操作者身份。用户的签名信息在每一个版本提交信息中能够看到，以此确认本次提交是水做的。$\textcolor{red}{GIt首次安装必须设置一下用户签名，否则无法提交代码。}$

$\textcolor{red}{注意:}$这里设置用户签名和将来登录GitHub的账号没有任何关系

### 初始化本地仓库

在需要设置仓库的文件路径下输入`git init`即可初始化本地库。

### 查看本地库状态

使用`git status`即可查看本地库状态。

![image-20230527142451296](http://cdn.t-terminal.icu/image-20230527142451296.png)

untracked files代表没有添加到暂存区的文件，git并没有追踪到，可以使用`git add 文件名`添加到暂存区。

![image-20230527142704028](http://cdn.t-terminal.icu/image-20230527142704028.png)

### 将文件从暂存区中删除

`git rm --cached 文件名`即可把文件从暂存区中删除。**只是从暂存区中删除，工作区中并没有删除。**

![image-20230527143312843](http://cdn.t-terminal.icu/image-20230527143312843.png)

### 提交到本地库

`git commit -m "日志信息"`即可将文件添加到本地库。

![image-20230527143542405](http://cdn.t-terminal.icu/image-20230527143542405.png)

使用`git reflog`可以查看提交信息。其中**fde23bf**就是本次提交的版本信息。

![image-20230527143611304](http://cdn.t-terminal.icu/image-20230527143611304.png)

`git log`不仅可以看到提交信息，也可以看到提交者。

![image-20230527143656927](http://cdn.t-terminal.icu/image-20230527143656927.png)

### 修改文件

如果文件在**提交到本地库后经过修改**，使用`git status`查看本地库状态时会显示修改后的文件，本地库状态会提示修改的文件。

![image-20230527144150500](http://cdn.t-terminal.icu/image-20230527144150500.png)

这时就需要重新提交修改的文件到本地库，然后本地库就的版本就会指向最新的提交版本。

![image-20230527144305126](http://cdn.t-terminal.icu/image-20230527144305126.png)

### 历史版本

`git reflog`可以查看版本信息。

`git log`可以看到版本详细信息。

#### 版本穿梭

步骤：

1. 通过`git reflog`查看版本号
2. 使用`git reset --hard 版本号`即可跳转到对应的版本，文件也会回退到对应的版本。

![image-20230527145412428](http://cdn.t-terminal.icu/image-20230527145412428.png)

**git切换版本，底层其实是移动的HEAD指针**。

![image-20230527145529361](http://cdn.t-terminal.icu/image-20230527145529361.png)

### 分支

在版本控制过程中，同时推进多个任务，为每个任务就可以创建单独的分支，使用分支意味着程序员可以把自己的工作从开发主线上分离开来，开发自己分支的时候，不会影响主线分支的运行。

#### 分支的操作

| 命令名称            | 作用                         |
| ------------------- | ---------------------------- |
| git branch -v       | 查看分支                     |
| git branch 分支名   | 创建分支                     |
| git checkout 分支名 | 切换分支                     |
| git merge 分支名    | 把指定的分支合并到当前分支上 |

![image-20230527151536894](http://cdn.t-terminal.icu/image-20230527151536894.png)

图中后面蓝色括号里的表示**当前分支**。

**$\textcolor{red}{每一个分支修改的文件仅在当前分支下有效，切换分支后，文件会变成对应分支的文件。}$**

hot-fix分支下的hello.txt文件。

<img src="http://cdn.t-terminal.icu/image-20230527151917828.png" alt="image-20230527151917828" />

master分支下的hello.txt文件。

![image-20230527152045684](http://cdn.t-terminal.icu/image-20230527152045684.png)

#### 合并分支

**master是主分支，合并分支要在master分支下进行合并！！！**

`git merge 分支名`

![image-20230527152314777](http://cdn.t-terminal.icu/image-20230527152314777.png)

#### 合并冲突

合并分支时，两个分支，在同一个文件的同一个位置有两套完全不同的修改。Git无法替我们决定使用哪一个，必须认为决定新代码内容。

![image-20230527153641423](http://cdn.t-terminal.icu/image-20230527153641423.png)

这时就要人为修改文件，决定文件的内容。

![image-20230527153729528](http://cdn.t-terminal.icu/image-20230527153729528.png)

![image-20230527153807711](http://cdn.t-terminal.icu/image-20230527153807711.png)

![image-20230527153833430](http://cdn.t-terminal.icu/image-20230527153833430.png)

## 远程仓库操作（github为例）

| 命令名称                           | 作用                                                     |
| ---------------------------------- | -------------------------------------------------------- |
| git remote -v                      | 查看当前所有远程地址别名                                 |
| git remote add 别名 远程地址       | 起别名，添加远程地址                                     |
| git remote rm 别名                 | 删除远程仓库                                             |
| git push 别名 分支                 | 推送本地分支上的内容到远程仓库                           |
| git clone 远程地址                 | 将远程仓库的内容克隆到本地                               |
| git pull 远程库地址别名 远程分支名 | 将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并 |



### 创建远程仓库别名

添加别名：`git remote add 别名 远程地址`

查看别名：`git remote -v`

![image-20230527155943429](http://cdn.t-terminal.icu/image-20230527155943429.png)

### 将本地库代码推送到远程库

`git push 别名 分支`

![image-20230527165708273](http://cdn.t-terminal.icu/image-20230527165708273.png)

### 将远程库代码下载到本地库

`git pull 别名 分支`

**获取到更新后的代码，使本地库代码与远程库代码同步。**

### 克隆远程库代码

`git clone 远程库地址`

**clone所做的事**

1. 拉取远程库的代码
2. 初始化本地仓库
3. 创建别名

### 团队协作

需要添加成员后，成员才能对代码进行推送。

![image-20230527171101146](http://cdn.t-terminal.icu/image-20230527171101146.png)

![image-20230527171122873](http://cdn.t-terminal.icu/image-20230527171122873.png)

![image-20230527171156033](http://cdn.t-terminal.icu/image-20230527171156033.png)

将随后生成的链接发给对方，**对方同意后**即可加入创作团队，进行代码推送。

## 远程仓库操作（SSH）

1. 创建SSH

   `ssh-keygen -t rsa -C github账号`即可生成ssh密钥。

2. 在C盘用户目录下的.ssh文件夹中即可看到公钥和私钥。

![image-20230527172728606](http://cdn.t-terminal.icu/image-20230527172728606.png)

**.pub是公钥，复制公钥，在github中添加公钥。**

![image-20230527172850431](http://cdn.t-terminal.icu/image-20230527172850431.png)



![image-20230527172914098](http://cdn.t-terminal.icu/image-20230527172914098.png)

![image-20230527172949732](http://cdn.t-terminal.icu/image-20230527172949732.png)

![image-20230527173053059](http://cdn.t-terminal.icu/image-20230527173053059.png)

3. 随后即可**通过SSH进行代码的拉取、推送等操作**

![image-20230527173129010](http://cdn.t-terminal.icu/image-20230527173129010.png)

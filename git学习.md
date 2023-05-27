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

![image-20230527142451296](C:\Users\Redmi\AppData\Roaming\Typora\typora-user-images\image-20230527142451296.png)

untracked files代表没有添加到暂存区的文件，git并没有追踪到，可以使用`git add 文件名`添加到暂存区。

![image-20230527142704028](C:\Users\Redmi\AppData\Roaming\Typora\typora-user-images\image-20230527142704028.png)

### 将文件从暂存区中删除

`git rm --cached 文件名`即可把文件从暂存区中删除。**只是从暂存区中删除，工作区中并没有删除。**

![image-20230527143312843](C:\Users\Redmi\AppData\Roaming\Typora\typora-user-images\image-20230527143312843.png)

### 提交到本地库

`git commit -m "日志信息"`即可将文件添加到本地库。

![image-20230527143542405](C:\Users\Redmi\AppData\Roaming\Typora\typora-user-images\image-20230527143542405.png)

使用`git reflog`可以查看提交信息。其中**fde23bf**就是本次提交的版本信息。

![image-20230527143611304](C:\Users\Redmi\AppData\Roaming\Typora\typora-user-images\image-20230527143611304.png)

`git log`不仅可以看到提交信息，也可以看到提交者。

![image-20230527143656927](C:\Users\Redmi\AppData\Roaming\Typora\typora-user-images\image-20230527143656927.png)

### 修改文件

如果文件在**提交到本地库后经过修改**，使用`git status`查看本地库状态时会显示修改后的文件，本地库状态会提示修改的文件。

![image-20230527144150500](C:\Users\Redmi\AppData\Roaming\Typora\typora-user-images\image-20230527144150500.png)

这时就需要重新提交修改的文件到本地库，然后本地库就的版本就会指向最新的提交版本。

![image-20230527144305126](C:\Users\Redmi\AppData\Roaming\Typora\typora-user-images\image-20230527144305126.png)

### 历史版本

`git reflog`可以查看版本信息。

`git log`可以看到版本详细信息。

#### 版本穿梭

步骤：

1. ​	通过`git reflog`查看版本号
2. 使用`git reset --hard 版本号`即可跳转到对应的版本，文件也会回退到对应的版本。
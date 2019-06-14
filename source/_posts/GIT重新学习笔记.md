title: GIT重新学习笔记
author: ismatch
tags:
  - GIT
categories: []
date: 2019-05-07 22:48:00
---
#### 0.重新系统学习GIT，查缺补漏

#### 1.关于版本控制
> 版本控制是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统

<!-- more -->

分类 | 定义| 典型作品
---|---|---
本地版本控制系统 | * | RCS
集中化的版本控制系统| 集中化的版本控制系统（Centralized Version Control Systems，简称 CVCS）。 这类系统，诸如 CVS、Subversion 以及 Perforce 等，都有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。|VSS SVN
分布式版本控制系统| 分布式版本控制系统（Distributed Version Control System，简称 DVCS）面世了。 在这类系统中，像 Git、Mercurial、Bazaar 以及 Darcs 等，客户端并不只提取最新版本的文件快照，而是把代码仓库完整地镜像下来。 这么一来，任何一处协同工作用的服务器发生故障，事后都可以用任何一个镜像出来的本地仓库恢复。 因为每一次的克隆操作，实际上都是一次对代码仓库的完整备份。| GIT

#### 2.GIT基础
- 直接记录快照，而非差异比较
- 近乎所有操作都是本地执行
    - 在 Git 中的绝大多数操作都只需要访问本地文件和资源，一般不需要来自网络上其它计算机的信息。
- Git 保证完整性
    - Git 中所有数据在存储前都计算校验和，然后以校验和来引用。
    -  使用SHA-1 散列生成校验和，类似于“24b9da6552252987aa493b52f8696cd6d3b00373”
- Git 一般只添加数据
- 三种状态
  * 已提交（committed）。表示数据已经安全的保存在本地数据库中。
  * 已修改（modified）。表示修改了文件，但还没保存到数据库中。
  * 已暂存（staged）。表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。
  * Git 仓库、工作目录以及暂存区域。
  ![image](https://git-scm.com/book/en/v2/images/areas.png)
- 基本的 Git 工作流程如下：

    * 在工作目录中修改文件。
    
    * 暂存文件，将文件的快照放入暂存区域。
    
    * 提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录。
    
#### 初次运行 Git 前的配置
- 外观和行为可通过配置变量进行配置。配置读取顺序，仓库 -> 当前用户 -> 所有用户（不大懂）
- 配置用户名称与邮件地址
```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

- 文本编辑器
    - 默认是vim编辑器
    - windows配置[notepad++]为默认编辑器
    ```
    // 配置 注意：'Program Files‘: 因为中间有空格，所以必须使用单引号括起来。
    $ git config --global core.editor  "C:/'Program Files'/Notepad++/Notepad++.exe"
    
    // 输出默认编辑器
    $ git config --global core.editor 
    ```
- 检查配置信息

```
git config --list
```

#### 3.操作仓库

- 在现有目录中初始化仓库
    - git init 。在现有目录（或者空目录）使用git bash键入该命令
    - git add -A 。添加所有文件（所有状态）
    - git add LICENSE 。添加许可证
    - git commit -m '你的提交信息'
    
- 克隆现有的仓库。
    ``` 
        $ git clone https://github.com/libgit2/libgit2
    ```
#### 4.记录每次更新到仓库

- 工作目录下的每一个文件都不外乎这两种状态：已跟踪或未跟踪
    - 已跟踪：已纳入版本控制，上一次快照有记录，目前处于未修改（unmodified），已修改（modified），已放入暂存区（staged）。
    - 未跟踪（Untracked files ）：工作目录中除已跟踪文件以外的所有其它文件都属于未跟踪文件
    - 初次克隆的项目，为已跟踪未修改状态。
        
- 生命周期了解。
- 检查当前文件状态。（status）
- 跟踪新文件。（add newfile.txt）
- 暂存已修改文件(add modified.txt)。所以git add是一个多功能命令，可以跟踪新文件，也可以把已跟踪文件放入暂存区，用于合并时把有冲突的文件标记为已解决的状态。git add这个命令理解为添加内容到下一次提交中”而不是“将一个文件添加到项目中”要更加合适
- 状态简览。（git status -s）
    - 新添加的未跟踪文件前面有 ?? 标记，新添加到暂存区中的文件前面有 A 标记，修改过的文件前面有 M 标记。
    
- 忽略文件。创建一个名为 .gitignore 的文件，列出要忽略的文件模式
    - [https://github.com/github/gitignore](https://github.com/github/gitignore)
    - 所有空行或者以 ＃ 开头的行都会被 Git 忽略。 
    - 可以使用标准的 glob 模式匹配。 
    - 匹配模式可以以（/）开头防止递归。 
    - 匹配模式可以以（/）结尾指定目录。 
    - 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。
    - 所谓的 glob 模式是指 shell 所使用的简化了的正则表达式。 星号（*）匹配零个或多个任意字符；[abc] 匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）；问号（?）只匹配一个任意字符；如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）。 使用两个星号（*) 表示匹配任意中间目录，比如 a/**/z 可以匹配 a/z , a/b/z 或 a/b/c/z 等。
    - 查看已暂存和未暂存的修改。(git diff)
    - 提交更新。git commit
    - 跳过使用暂存区域。git commit -a -m 'added new benchmarks'
    - 移除文件。从已跟踪文件清单中移除。git rm
        -  手工删除文件
        - 把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中
    - 移动文件
    
#### 学习地址
- [官网地址](https://git-scm.com/book/zh/v2/)    
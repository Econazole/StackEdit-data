

## git
```
严明伟
http://sswiki.sigmastar.com.tw:8090/pages/viewpage.action?pageId=37958095
```

[runoob git教程](https://www.runoob.com/git/git-workspace-index-repo.html)
[runoob 图解git](https://www.runoob.com/w3cnote/git-graphical.html)

抽象，具体的结合，比如说工作区具体是在linux的目录下的哪里。

**Git 的工作就是创建和保存你的项目的快照及与之后的快照进行对比。**

![输入图片说明](/imgs/2024-04-18/72KV0PIYBZsgMIES.png)

![输入图片说明](/imgs/2024-04-21/iCZ94qgrA2RTURoG.png)

![输入图片说明](/imgs/2024-04-19/LXzSB0ZQChMDYNvx.png)

-   workspace：工作区，在当前目录下`git init`，生成了`.git`文件夹，当前目录除此文件夹外的区域就是工作区
-   staging area：暂存区/缓存区，是`./git/index`，是一个文件，`git commit`会将暂存区内容添加到本地仓库中，实际会添加到目录`./git/objects`中。
-   local repository：版本库或本地仓库，就是隐藏目录`.git`
-   remote repository：远程仓库

### git基本操作
[runoob git基本操作](https://www.runoob.com/git/git-basic-operations.html)

- `git init`：只用于在一个**空目录**中创建新仓库，如果你想要 clone 一个已存在的远程仓库到本地，请使用 [git clone](https://www.runoob.com/git/git-clone.html) 命令；执行后默认情况下 Git 就会为你创建 **master** 分支。

- **git status** 命令可以查看在你上次提交之后是否有对文件进行再次修改（包括新增/修改..）
git status -s

- 文件修改后，我们一般都需要进行 `git add` 命令将其添加到缓存中，从而保存历史版本。

- `git clone` 会复制远程git仓库的全部记录，包括`.git`目录

- `git diff` 命令比较文件的不同，即**比较文件在暂存区和工作区的差异**。`git status` 显示你上次提交更新后的更改或者写入缓存的改动， 而 `git diff` 一行一行地显示这些改动具体是啥。

- `git commit -m [message即备注信息]` 命令将暂存区内容添加到本地仓库中。本质是记录快照。备注信息可以写“add/removed file1 file2”这种

- `git reset` 命令用于回退版本，可以指定退回某一次提交的版本/快照。
	- 语法格式：`git reset [--soft | --mixed | --hard] [HEAD]`
	- **--mixed** 为默认，可以不用带该参数，用于**重置暂存区的文件**与上一次的提交(commit)保持一致，**工作区文件内容保持不变**。实例：
		```bash
		$ git reset HEAD^            # 回退所有内容到上一个版本  
		$ git reset HEAD^ hello.php  # 回退 hello.php 文件的版本到上一个版本  
		$ git  reset  052e           # 回退到指定版本
		```
	- **--soft** 参数用于回退到某个版本：
		`$ git reset --soft HEAD~3   # 回退上上上一个版本`
	- **--hard** 参数撤销工作区中所有未提交的修改内容，**将暂存区与工作区都回到上一次版本**，并删除之前的所有信息提交：
		```bash
		$ git reset --hard HEAD~3  # 回退上上上一个版本  
		$ git reset –hard bae128  # 回退到某个版本回退点之前的所有信息。 
		$ git reset --hard origin/master    # 将本地的状态回退到和远程的一样 
		```
	- `git reset HEAD [file]` 以取消之前 git add 添加，但不希望包含在下一提交快照中的缓存。可以理解成撤销某个文件的`git add`的添加缓存的操作

- `git blame <file>`：以**列表形式**查看指定文件的历史修改记录。

- `git log [选项] [分支名/提交哈希]`：显示从最新提交到最早提交的所有提交信息，包括提交的哈希值、作者、提交日期和提交消息等。
	- `--oneline`：以简洁的一行格式显示提交信息
	- `--graph`：以图形化方式显示分支和合并历史

- `git remote add <remote_name> <remote_url>`：`<remote_name>`是要添加的远程仓库的名称。通常，远程仓库的名称为 `origin`，但你也可以自定义一个名称。添加远程仓库后，才可以使用其他 Git 命令与远程仓库进行交互，例如`git push` 推送本地代码到远程仓库、`git pull` 拉取远程仓库的代码等。

### Git 分支管理

![输入图片说明](/imgs/2024-04-21/zGsp6604jQ6idDPl.png)

一个分支代表一条独立的开发线，使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的同时继续工作。

节点是commit，分支/树干是branch，主干是master。
**Git 分支实际上是指向更改快照的指针。**
当你切换分支的时候，Git 会用**该分支的最后提交的快照**替换你的**工作目录的内容**

![输入图片说明](/imgs/2024-04-18/lW7B6W1RrD8kMer4.png)

分支合并冲突

## Repo
官方的定义：Repo是谷歌用Python脚本写的调用git的一个脚本，可以实现管理多个git库。

个人理解：repo这个工具，是一个脚本。这个脚本是对git库的管理。
类似什么呢，类似makfile。功能是使你简单一敲make，就ok了。repo 呢，简单一敲，repo init -u <url> <option> 。
url 指的是 manifest仓库地址，option 一般是所在分支，比如-b 你的分支，就行了。再执行一句，repo sync 。刷刷刷，等待个几十个小 时，（网速好的，时间相对短一点）。就把你需要的安卓整个源码同步在本地了（几十个G这么大吧）。

值得提一下的是，为什么有repo这个功能。
repo呢，其实来说，就是很多个git clone 的集成，如果有一个工程，有一百个git，你下载下来，按逻辑是敲一百次git clone xxxx，下载下来。但是使用repo呢，只需要敲一次，喝喝茶，等待下载完成就可以了。

**分析 .xml 文件**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>

<remote name="aosp"
fetch=".."
review="https://android-review.googlesource.com/" />

<default revision="master"
remote="aosp"
sync-j="4" />

<project path="build" name="platform/build" groups="pdk,tradefed" >
<copyfile src="core/root.mk" dest="Makefile" />
</project>

<project path="abi/cpp" name="platform/abi/cpp" groups="pdk" />
<project path="art" name="platform/art" groups="pdk" />
...
<project path="tools/studio/translation" name="platform/tools/studio/translation" groups="notdefault,tools" />
<project path="tools/swt" name="platform/tools/swt" groups="notdefault,tools" />

</manifest>
```
\<remote\>：描述了远程仓库的基本信息。
- `name`描述的是一个远程仓库的名称，通常我们看到的命名是origin; 名字自己起，用于区分多个 `remote`，git pull、get fetch的时候会用到这个remote name
- `fetch`用作项目名称的前缘，指定了从哪里获取仓库的元数据。这里指定从当前目录(`..`)获取仓库的元数据。
- `review`描述的是用作code review的server地址

\<default\>：default标签的定义的属性，将作为`<project>`标签的默认属性，在`<project>`标签中，也可以重写这些属性。
- 属性`revision`表示当前的版本，也就是我们俗称的分支;
- 属性`remote`描述的是默认使用的远程仓库名称，即`<remote>`标签中name的属性值；
- 属性`sync-j`表示在同步远程代码时，并发的任务数量，配置高的机器可以将这个值调大

\<project\>：每一个repo管理的git库，就是对应到一个`<project>`标签，
- path描述的是项目相对于远程仓库URL的路径，同时将作为对应的git库在本地代码的路径; 
- name用于定义项目名称，命名方式采用的是整个项目URL的相对地址。 譬如，AOSP项目的URL为https://android.googlesource.com/，命名为platform/build的git库，访问的URL就是https://android.googlesource.com/platform/build

[csdn 一张图让你掌握清单文件manifest.xml的重点](https://blog.csdn.net/guyongqiangx/article/details/113526601)
[csdn Repo manifests默认default.xml清单文件中的各个标签详解](https://blog.csdn.net/ezconn/article/details/132473051)
搞清楚两个点：从哪下，下到哪
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjU2NjcwNTFdfQ==
-->
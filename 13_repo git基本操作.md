
```
严明伟
http://sswiki.sigmastar.com.tw:8090/pages/viewpage.action?pageId=37958095
```

菜鸟教程：https://www.runoob.com/git/git-workspace-index-repo.html


![输入图片说明](/imgs/2024-04-18/72KV0PIYBZsgMIES.png)

节点是commit，树干是branch，主干是master

![输入图片说明](/imgs/2024-04-18/lW7B6W1RrD8kMer4.png)

**Repo**
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
- name描述的是一个远程仓库的名称，通常我们看到的命名是origin;
- fetch用作项目名称的前缘，指定了从哪里获取仓库的元数据。在构造项目仓库远程地址时使用到;
- review描述的是用作code review的server地址

\<default\>：default标签的定义的属性，将作为`<project>`标签的默认属性，在`<project>`标签中，也可以重写这些属性。
- 属性revision表示当前的版本，也就是我们俗称的分支;
- 属性remote描述的是默认使用的远程仓库名称，即`<remote>`标签中name的属性值；
- 属性sync-j表示在同步远程代码时，并发的任务数量，配置高的机器可以将这个值调大

\<project\>：每一个repo管理的git库，就是对应到一个`<project>`标签，
- path描述的是项目相对于远程仓库URL的路径，同时将作为对应的git库在本地代码的路径; 
- name用于定义项目名称，命名方式采用的是整个项目URL的相对地址。 譬如，AOSP项目的URL为https://android.googlesource.com/，命名为platform/build的git库，访问的URL就是https://android.googlesource.com/platform/build

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM1OTE3MzMwM119
-->
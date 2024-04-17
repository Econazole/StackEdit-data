[TOC]

## grep
`grep`是一个在Linux和Unix系统中用于搜索文本的命令行工具。它可以在文件中查找特定的字符串模式，并输出包含匹配的行。

下面是几个常用的`grep`选项及其解释：

1. `-r` 或 `--recursive`:
   - 递归搜索指定目录下的所有子目录。
   - 示例：
     ```bash
     grep -r "example" /path/to/directory/
     ```
     这会在`/path/to/directory/`及其所有子目录中搜索包含“example”的行。

2. `-n` 或 `--line-number`:
   - 显示匹配行的行号。
   - 示例：
     ```bash
     grep -n "pattern" filename.txt
     ```
     这会在`filename.txt`中搜索“pattern”，并显示包含该模式的行号。

3. `-w`:
   - 只匹配整个单词，而不是单词的部分。
   - 示例：
     ```bash
     grep -w "word" filename.txt
     ```
     这会在`filename.txt`中搜索完全匹配“word”的行。

4. `-l` 或 `--files-with-matches`:
   - 只列出包含匹配内容的文件名，而不显示匹配的具体行。
   - 示例：
     ```bash
     grep -l "pattern" /path/to/directory/*
     ```
     这会在`/path/to/directory/`下的所有文件中搜索“pattern”，并列出包含匹配内容的文件名。

这些选项可以单独使用或结合使用，以便更精确地搜索和过滤输出结果。

## find
`find`是一个强大的命令行工具，用于在文件系统中搜索文件和目录。它可以根据各种条件搜索文件，并执行相应的操作，如打印、删除、修改等。

下面是一些常用的`find`选项及其解释：

1. `-name`:
   - 根据文件名模式搜索文件。
   - 示例：
     ```bash
     find /path/to/directory -name "*.txt"
     ```
     这会在`/path/to/directory`目录及其子目录中搜索所有以`.txt`结尾的文件。

2. `-type`:
   - 根据文件类型搜索，如普通文件（`f`）、目录（`d`）、符号链接（`l`）等。
   - 示例：
     ```bash
     find /path/to/directory -type d
     ```
     这会在`/path/to/directory`目录中搜索所有子目录。

3. `-size`:
   - 根据文件大小搜索。
   - 示例：
     ```bash
     find /path/to/directory -size +1M
     ```
     这会在`/path/to/directory`目录及其子目录中搜索大小大于1MB的文件。

4. `-exec`:
   - 对搜索到的每个文件执行指定的命令。
   - 示例：
     ```bash
     find /path/to/directory -name "*.txt" -exec cp {} /path/to/destination/ \;
     ```
     这会在`/path/to/directory`目录中搜索所有以`.txt`结尾的文件，并将它们复制到`/path/to/destination/`目录。

5. `-mtime` 和 `-mmin`:
   - 根据文件的修改时间搜索。
   - 示例：
     ```bash
     find /path/to/directory -mtime -7
     ```
     这会在`/path/to/directory`目录及其子目录中搜索在最近7天内修改过的文件。

6. `-maxdepth` 和 `-mindepth`:
   - 控制搜索的深度。
   - 示例：
     ```bash
     find /path/to/directory -maxdepth 2 -name "*.txt"
     ```
     这会在`/path/to/directory`及其直接子目录中搜索所有以`.txt`结尾的文件，但不会搜索更深的子目录。

这些选项可以结合使用，以创建复杂的搜索条件，满足各种文件搜索需求。

---
## Q 文件系统的含义
Linux下硬链接只有在同一个文件系统中才能创建，请问什么是同一个文件系统？

在Linux系统中，文件系统是用于组织和管理存储设备（如硬盘、分区、USB驱动器等）上的数据的方式。每个文件系统都有一个唯一的标识符，称为文件系统标签或UUID。

“同一个文件系统”指的是所有硬链接和目标文件必须位于同一个文件系统标识符或UUID下。如果它们不是同一个文件系统，那么创建硬链接就是不可能的。

这里有几点关于文件系统的说明：

1. **EXT3、EXT4等**：这些是Linux常见的本地文件系统，每个都有自己的UUID。

2. **VFAT、NTFS等**：这些是Windows和Linux都支持的文件系统，每个也有自己的UUID。

3. **文件系统挂载**：当你将一个存储设备挂载到Linux文件系统中时，它会被分配一个挂载点，通常是一个目录。只有在同一个挂载点下的文件才能创建硬链接。

例如，如果你有一个外部USB驱动器挂载到`/media/mydrive`，那么`/media/mydrive/file1`和`/media/mydrive/file2`是在同一个文件系统上，因此可以创建硬链接。

如果你想要创建硬链接，但目标文件位于不同的文件系统，你可以考虑使用符号链接（symbolic link，即软链接），它可以跨越文件系统和设备边界。

---
## 链接
http://linux.devonline.net/c/ln.html

---
## chgrp 和 chown 的区别
`chgrp`和`chown`都是Linux命令，用于更改文件或目录的所有权和权限，但它们更改的是不同的属性：

1. **chgrp**:
   - **功能**: 更改文件或目录的所属组。
   - **用法**: `chgrp [选项] 组名 文件或目录`
   - **例子**: 
     ```bash
     chgrp users file.txt
     ```
     这会将`file.txt`的所属组更改为`users`。

2. **chown**:
   - **功能**: 更改文件或目录的所有者和所属组。
   - **用法**: `chown [选项] [所有者]:[组名] 文件或目录`
   - **例子**:
     ```bash
     chown john:users file.txt
     ```
     这会将`file.txt`的所有者更改为`john`，并将所属组更改为`users`。

**总结**:
- `chgrp`更改文件或目录的所属组，但不改变所有者。
- `chown`更改文件或目录的所有者和所属组。

这两个命令都可以与其他选项结合使用，以递归地更改目录中的文件和子目录的所有权，以及在更改时提供更多的控制和反馈。

---
## free
用于查看系统内存使用情况的命令
**`-h`**: “human-readable”。使用这个选项，`free`将以更容易阅读的格式显示内存使用情况，即以适当的单位（如KB、MB、GB）来显示内存的大小，而不是以字节

---
## fiile
`file`是一个用于确定文件类型的命令行工具。它可以识别文件的内容，不仅仅是通过文件扩展名，这使得它在处理不带扩展名的文件或具有未知扩展名的文件时非常有用。

以下是`file`命令的基本用法和一些示例：

**基本用法**
```bash
file [选项] 文件名
```

**常用选项**
- `-b` 或 `--brief`: 只显示文件类型，不显示文件名。
- `-i` 或 `--mime`: 显示MIME类型。
- `-z`: 对压缩文件进行检查。
- `-z`: 仅对压缩文件进行检查。
- `-L`: 对符号链接的目标进行检查，而不是符号链接本身。
- `-d`: 对目录进行检查，而不是目录中的内容。

**示例**
1. **查看文件类型**
   ```bash
   file filename.txt
   ```
   输出可能是类似于`filename.txt: ASCII text`，表示该文件是一个ASCII文本文件。

2. **查看MIME类型**
   ```bash
   file -i image.jpg
   ```
   输出可能是类似于`image.jpg: image/jpeg`，表示该文件是一个JPEG图像。

3. **检查压缩文件**
   ```bash
   file -z archive.tar.gz
   ```
   如果`archive.tar.gz`是一个gzip压缩的tar文件，输出可能是类似于`archive.tar.gz: gzip compressed data, tar archive`。

`file`命令对于确定文件的类型非常有用，特别是当文件扩展名不可用或不可靠时。它可以识别多种文件类型，包括文本文件、二进制文件、图像、音频、视频等。

---
## md5
**md5sum命令** 采用MD5报文摘要算法（128位）计算和检查文件的校验和。
MD5算法常常被用来验证网络文件传输的完整性，防止文件被人篡改。

**检查文件testfile是否被修改过：**

首先生成md5文件：

```shell
md5sum testfile > testfile.md5
```

检查：

```shell
md5sum testfile -c testfile.md5
```

如果文件没有变化，输出应该如下：

```shell
forsort: OK
```

此时，md5sum命令返回0。

如果文件发生了变化，输出应该如下：

```shell
forsort: FAILED
md5sum: WARNING: 1 of 1 computed checksum did NOT match
```

此时，md5sum命令返回非0。

---
## diff：对比文件差异

**以正常模式比较差异**
```bash
diff a.txt b.txt
```

**以上下文 (context) 模式比较差异**
```bash
diff -c a.txt b.txt
```

```bash
　　*** a1.txt 2012-08-29 16:45:41.000000000 +0800
　　--- a2.txt 2012-08-29 16:45:51.000000000 +0800
　　***************
　　*** 1,7 ****
　　 a
　　 a
　　 a
　　!a
　　 a
　　 a
　　 a
　　--- 1,7 ----
　　 a
　　 a
　　 a
　　!b
　　 a
　　 a
　　 a
```

**以联合 (unified) 模式比较差异**
```bash
diff -u a.txt b.txt
```

```bash
　　--- a.txt 2012-08-29 16:45:41.000000000 +0800
　　+++ b.txt 2012-08-29 16:45:51.000000000 +0800
　　@@ -1,7 +1,7 @@
　　 a
　　 a
　　 a
　　-a
　　+b
　　 a
　　 a
　　 a
```

---
## tar
`tar`是一个在Unix和Linux系统中用于归档和压缩文件的命令行工具。它可以将多个文件或目录打包成一个单一的文件，并可选地进行压缩。以下是`tar`命令中一些常用选项的解释：

**基本用法**
```bash
tar [选项] [文件或目录...]
```

**常用选项**
1. **`-c` 或 `--create`**:
   - **功能**: 创建新的归档文件。
   - **示例**:
     ```bash
     tar -cf archive.tar file1.txt file2.txt
     ```
     这会创建一个名为`archive.tar`的新归档文件，并包含`file1.txt`和`file2.txt`。

2. **`-v` 或 `--verbose`**:
   - **功能**: 显示详细的操作信息。
   - **示例**:
     ```bash
     tar -cvf archive.tar file1.txt file2.txt
     ```
     `-v`选项会在打包过程中显示文件名，以便你可以看到哪些文件正在被添加到归档中。

3. **`-f` 或 `--file`**:
   - **功能**: 指定归档文件的名称。
   - **示例**:
     ```bash
     tar -cvf archive.tar file1.txt file2.txt
     ```
     `-f`后面跟着的是归档文件的名称。

4. **`-z` 或 `--gzip`**:
   - **功能**: 使用gzip压缩归档文件。
   - **示例**:
     ```bash
     tar -czvf archive.tar.gz directory/
     ```
     这会创建一个gzip压缩的归档文件`archive.tar.gz`，其中包含`directory/`目录中的所有文件。

5. **`-x` 或 `--extract`**:
   - **功能**: 解压归档文件。
   - **示例**:
     ```bash
     tar -xvf archive.tar
     ```
     这会解压`archive.tar`文件到当前目录。

这些选项可以结合使用，以创建、查看、压缩和解压归档文件，满足各种文件管理和数据备份需求。

**zip格式**
压缩： zip -r [目标文件名].zip [原文件/目录名]  
解压： unzip [原文件名].zip  
注：-r参数代表递归

---
## mount
`mount`和`umount`是Linux和Unix系统中用于挂载和卸载文件系统的命令行工具。

**mount**
`mount`命令用于将Linux系统外的文件系统挂载到指定的挂载点（目录）上。
在Linux系统中，文件系统可以是磁盘分区、USB驱动器、网络文件系统（如NFS）等。

**基本用法**
```bash
mount [选项] 设备 挂载点
```

**示例**
1. **挂载分区**
	```bash
	   mount /dev/sdb1 /mnt/mydrive
	```
   这会将`/dev/sdb1`分区挂载到`/mnt/mydrive`目录上。

2. **挂载ISO文件**
	```bash
	   mount -o loop image.iso /mnt/cdrom
	```
   这会将`image.iso`文件挂载为一个虚拟CDROM到`/mnt/cdrom`目录上。

**umount**
`umount`命令用于卸载（解除挂载）已挂载的文件系统。

**基本用法**
```bash
umount [选项] 挂载点
```

**示例**
1. **卸载分区**

   ```bash
   umount /mnt/mydrive
   ```

   这会从`/mnt/mydrive`目录上卸载已挂载的文件系统。

2. **卸载所有挂载的文件系统**

   ```bash
   umount -a
   ```

   这会卸载所有已挂载的文件系统，除了`/`和`/proc`。

 **常用选项**
- `-a`: 卸载所有已挂载的文件系统。
- `-t 文件系统类型`: 指定要卸载的文件系统类型。

**注意事项**
- 在卸载文件系统之前，请确保没有任何进程正在使用该文件系统，否则可能会导致数据丢失或文件系统损坏。
- 在卸载之前，确保没有当前目录或其他进程正在使用挂载点上的文件。

`mount`和`umount`命令是系统管理员和高级用户在管理和维护文件系统时常用的工具。正确使用这些命令可以确保文件系统的稳定性和数据完整性。

---
## sed
可用于文本的解析转换，在不打开文件的情况下编辑文本内容
**sed 命令是面向“行”处理的，每一次处理一行内容。**处理时，把当前处理的行存储在临时缓冲区中，称为“模式空间”（pattern space），接着用sed命令处理缓冲区中的内容，处理完成后，把缓冲区的内容送往屏幕。接着处理下一行，这样不断重复，直到文件末尾。**在这个处理过程中，sed 命令并不会对文件本身进行任何更改，除非你使用重定向存储输出**。

---
## awk脚本基本结构

```bash
awk 'BEGIN{ print "start" } pattern{ commands } END{ print "end" }' file
```

一个awk脚本通常由：BEGIN语句块、能够使用模式匹配的通用语句块、END语句块3部分组成，这三个部分是可选的。任意一个部分都可以不出现在脚本中，脚本通常是被 **单引号** 中，例如：

```bash
awk 'BEGIN{ i=0 } { i++ } END{ print i }' filename
```

**awk的工作原理**
```bash
awk 'BEGIN{ commands } pattern{ commands } END{ commands }'
```

-   第一步：执行`BEGIN{ commands }`语句块中的语句；
-   第二步：从文件或标准输入(stdin)读取一行，然后执行`pattern{ commands }`语句块，它逐行扫描文件，从第一行到最后一行重复这个过程，直到文件全部被读取完毕。
-   第三步：当读至输入流末尾时，执行`END{ commands }`语句块。

**BEGIN语句块** 在awk开始从输入流中读取行 **之前** 被执行，这是一个可选的语句块，比如变量初始化、打印输出表格的表头等语句通常可以写在BEGIN语句块中。

**END语句块** 在awk从输入流中读取完所有的行 **之后** 即被执行，比如打印所有行的分析结果这类信息汇总都是在END语句块中完成，它也是一个可选语句块。

**pattern语句块** 中的通用命令是最重要的部分，它也是可选的。如果没有提供pattern语句块，则默认执行`{ print }`，即打印每一个读取到的行，awk读取的每一行都会执行该语句块。

---
## xargs
xargs能够捕获一个命令的输出，然后传递给另外一个命令
之所以能够用到这个命令，是因为很多命令不支持管道来传递参数，而日常工作中有这个必要，所以就有了xargs命令
find /sbin -perm +700 | ls -l				#错误
find /sbin -perm +700 | xargs ls -l	#正确

---
## shell脚本
![输入图片说明](/imgs/2024-04-17/W8RzoGbGoEe6t5ol.png)

## 练习
linux命令：
1. 举例如何查找当前目录下的.c文件？
	`find . -type f -name "*.c"`

2. 举例如何找出当前目录下.log中， 包含fail子串的文件及其对应行数？请将查找结果并将全部结果保存进文件。
	`grep -rn "fail" *.log > results.txt`

3. 举例如何快速将当前.ini文件中的“PASS”，替换为Pass?
	`sed -i 's/PASS/Pass/g' filename.ini`
	解释：
	`-i`: “in-place”。使用这个选项，`sed`将直接在原始文件中进行替换
	`'s/PASS/Pass/g'`: 这是`sed`的替换命令：
	-   **`s`**: 表示替换操作。
	-   **`PASS`**: 是你想要查找并替换的模式。在这里，它查找大写的“PASS”。
	-   **`Pass`**: 是替换模式。当找到匹配的“PASS”时，它将被替换为“Pass”。
	-   **`g`**: 是一个标志，表示全局替换。这意味着它将替换每一次出现的“PASS”，而不仅仅是第一次出现

4. 举例分别使用zip/tar对文件进行压缩归档，并给出对应的解压缩命令
    -   使用`zip`：
        `zip archive_name.zip file1 file2 file3`
        **解压缩：**
        `unzip archive_name.zip`

    -   使用`tar`：
        `tar -czvf archive_name.tar.gz file1 file2 file3`
        **解压缩：**
        `tar -xzvf archive_name.tar.gz`
        
5. 如何将文件打包压缩为gzip/bzip2? 如何解压？
	-   **gzip**: 
	    **压缩：**
	    `gzip filename`
	    **解压：**
	    `gunzip filename.gz`
	    
	-   **bzip2**:
	    **压缩：**
	    `bzip2 filename`
	    **解压：**
	    `bunzip2 filename.bz2`
	    
6. 举例说明软链接与硬链接的区别
	- **软链接**：指向文件的路径，文件删除时，链接失效。
	- **硬链接**：指向文件的物理数据块，文件删除时，数据仍存在。

7. 如何检查一个文件的md5使用
	`md5sum filename`

8. 如何获取当前路径？ 如何查看系统正在运行的进程？ 如何查看当前系统剩余的内存数
	`pwd / ps -aux / free -h`
9. Bash:
	通过一个shell脚本,完成：
	(1) 解压文件：test.xxx
	(2) 同时找到以xxx_test_case_00x命名的文件， 改为xxx_tc00x
	(3) 找出所有名叫“Makefile”的文件，改名为run.mk
	(4) 将run.mk中的“nop=true” 替换为"nop=false"
	
	```bash
	#!/bin/bash
	# (1) 解压文件：test.xxx
	unzip test.xxx

	# (2) 同时找到以xxx_test_case_00x命名的文件，改为xxx_tc00x
	rename 's/_test_case_00(\d{1})/_tc0$1/' *test_case_00*
	# `-exec`选项允许我们执行一个命令来对这些文件进行操作
	
	# (3) 找出所有名叫“Makefile”的文件，改名为run.mk
	find . -type f -name "Makefile" -exec rename 's/Makefile/run.mk/' {} +

	# (4) 将run.mk中的“nop=true” 替换为"nop=false"
	sed -i 's/nop=true/nop=false/g' run.mk
	```


	

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MTQxNTU2NzldfQ==
-->
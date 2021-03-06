---
title: Ubuntu 中 chmod 改变权限
category: linux
description: Ubuntu 中使用 chmod 改变文件的权限
keywords: ubuntu,linux,chmod,改变权限
---

以下的内容摘录于 鸟哥的linux私房菜 并结合了自己的理解。

文件权限的改变使用的是 chmod 这个命令，但是权限的设置方法有两种:

1. 使用数字来进行权限的更改
2. 使用符号来进行权限的更改

先介绍一点需要的基础知识：

linux 基本权限有9个，分别是 owner,group, others 三种身份各有自己的 read、write、execute 权限。

- 数字类型改变权限

    各权限的数字代表为:
    
    - r: 4
    - w: 2
    - x: 1
    
    此时的 chmod 命令的语法为:
    
        chomod [-R] xyz 文件或目录
        参数简介:
        
        xyz: 就是刚刚提到的数字类型的权限属性，每一个分别代表的是每一种身份的人的属性数值相加结果
        -R: 进行递归的持续修改，即连同子目录下的所有文件都会更改
        
    看看例子吧：
    
    常常我们以 vim 编辑一个 shell 的文件批处理文件后，它的权限通常是 `-rw-rw-r--`，也就是 `664`，如果要将该文件变成可执行文件，并且不让其他人修改次文件的话，那么就需要 `-rwxr-xr-x` 这样的权限，此时就要执行 `chmod 755 test.sh` 命令。

- 符号类型改变权限

    在这种改变权限的方法中，通过使用如下的规则来代替身份:
    
    - u: users
    - g: group
    - o: others
    - a: all the above
    
    语法规则为:
    
        chmod [ugoa] [+-=] [rwx] [filename or directory]
        
        参数简介：
        
        +: 代表的是文件或目录的其它属性不改变，仅增加指定的属性
        -: 代表的是文件或目录的其它属性不改变，仅减去指定的属性
        =: 代表的是文件或目录的属性设置为指定的属性
        
    看看例子应该就明白了:
    
    还是采用上面的 shell 文件权限的处理吧，如果文件的权限是 `-rw-rw-r--`，这个时候如果要让这个文件变成可执行文件，只需要执行 `chmod a+x test.sh` 就可以了，这个时候文件的权限就被更改为 `-rwxrwxr-x` 。
    
欢迎指教=^_^=

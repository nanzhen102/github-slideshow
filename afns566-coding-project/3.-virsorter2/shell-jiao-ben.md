# 3.2 Shell

#### 3.2.1 Introduction

1\) The bash shell

**Shell** provides an interface between the user and the kernel \(The core of Linux operating system\).

**Bash** is the shell, or command language interpreter, for the Linux operating system. 

2\) Shell scripting

A **shell script** is a text file containing a sequence of commands, so it tells the shell to execute those commands instead of entering the commands line by line.

**Shell keywords** such as if..else, do..while. **Shell commands** such as pwd, test, echo, continue, type.

3\) Variables in shell





#### 3.2.2 SHELL变量

```text
(base) [nanzhen@admin ~]$ echo $SHELL
>>> /bin/bash
```

可以发现当前系统已经默认使用**Bash作为命令行终端解释器**。

{% hint style="info" %}
shell是一个变量，所以$SHELL

但，大写？！

`echo` 在终端输出字符串或变量提取后的值

`echo [字符串 | $变量 ]`

Bash 是目前最常用的 Shell，除非特别指明，Shell == Bash，可以互换。用户可以通过`bash`命令的`--version`参数或者环境变量`$BASH_VERSION`，查看本机的 Bash 版本。

`bash --version` 或`echo $BASH_VERSION`
{% endhint %}

#### **3.2.3** 简单的脚本编写

使用Vim编辑器把Linux命令按照顺序依次写入到一个文件中，这就是一个简单的脚本。

Shell脚本文件的名称可以任意，但为了避免被误以为是普通文件，建议将.sh后缀加上，以表示是一个脚本文件。

**Step1.** vim新建脚本文档，.sh后缀

`vim practice_bash.sh`

**Step2.** vim输入模式，按顺序输入Linux命令

```text
#!/bin/bash
# you can add some comments here. they will be ignored.
pwd
ls -al
~                                                                                                                   
~  
~                                                                                                                 
"practice_bash.sh" 4L, 24C    
```

The **\#! syntax** used in scripts to indicate an interpreter for execution under Linux operating systems. Most Linux shell and python script starts with `#!/bin/bash` or `#!/usr/bin/python3`. 

A word or line beginning with **\#** causes that word and all remaining characters on that line to be ignored. It helps other system admins to understand your code, logic and it helps them to modify the script you wrote.

**Step3.** vim退出

先Esc

再末行模式，`:wq!`

**Step4.** 执行脚本

`bash practice_bash.sh`



#### 3.2.4 References

* https://www.linuxprobe.com/chapter-04.html
* https://github.com/qinjx/30min\_guides/blob/master/shell.md
* https://bash.cyberciti.biz/guide/Main\_Page  **👈  ✨✨**  
* https://linuxcommand.org/lc3\_writing\_shell\_scripts.php **👈  ✨✨** 




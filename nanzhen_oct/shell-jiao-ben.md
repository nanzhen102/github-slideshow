# 2. Shell脚本

#### 2.1 Introduction

Shell**终端解释器**是人与计算机硬件之间的“翻译官”，它作为用户与Linux系统内部的通信媒介，除了能够支持各种变量与参数外，还提供了诸如循环、分支等高级编程语言才有的控制结构特性。要想正确使用Shell中的这些功能特性，**准确下达命令**尤为重要。

Shell**脚本命令**的工作方式有两种：交互式（Interactive）和批处理（Batch）。

{% tabs %}
{% tab title="Interactive" %}
用户每输入一条命令就立即执行
{% endtab %}

{% tab title="Batch（Recommended）" %}
由用户事先编写好一个完整的Shell script（脚本），Shell会一次性执行脚本中诸多的命令
{% endtab %}
{% endtabs %}

#### 2.2 SHELL变量

```text
(base) [nanzhen@admin ~]$ echo $SHELL
>>> /bin/bash

```

可以发现当前系统已经默认使用**Bash作为命令行终端解释器**。

{% hint style="info" %}
shell是一个变量，所以$SHELL

但，大写？

`echo` 在终端输出字符串或变量提取后的值

`echo [字符串 | $变量 ]`

Bash 是目前最常用的 Shell，除非特别指明，Shell == Bash，可以互换。用户可以通过`bash`命令的`--version`参数或者环境变量`$BASH_VERSION`，查看本机的 Bash 版本。

`bash --version` 或`echo $BASH_VERSION`
{% endhint %}

#### 2.3 **简单的脚本编写**

使用Vim编辑器把Linux命令按照顺序依次写入到一个文件中，这就是一个简单的脚本。

Shell脚本文件的名称可以任意，但为了避免被误以为是普通文件，建议将.sh后缀加上，以表示是一个脚本文件。

**Step1. vim新建脚本文档，.sh后缀**

`vim practice_bash.sh`

**Step2. vim输入模式，按顺序输入Linux命令**

```text
#!/bin/bash
pwd
ls -al
~                                                                                                                   
~  
~                                                                                                                 
"practice_bash.sh" 4L, 24C    
```

第一行的脚本声明（\#!）用来告诉系统使用哪种Shell解释器来执行该脚本

第二、三行的可执行语句是我们平时执行的Linux命令

此外，其他行也可以可以（\#），表示注释信息，对脚本功能和某些命令进行介绍

**Step3. vim退出**

先Esc

再末行模式，`:wq!`

**Step4. 执行脚本**

`bash practice_bash.sh`

#### 2.4 复杂脚本，SHELL内置变量等



#### 2.5 References

* https://www.linuxprobe.com/chapter-04.html




# 3.2 Vim Text Editor

#### 1.1 Introduction

编写脚本文档

#### 1.2 进入vim编辑器

**Step1.** 打开／新建（临时），Vim编辑器命令模式

```
(base) [nanzhen@admin ~]$ vim practice_vim.txt
```

**Step2.** Vim编辑器命令模式——输入模式（编辑）

a 光标后面一位

i 光标当前位置

o 光标的下面再创建一个空行

{% hint style="info" %}
a. 命令模式下，不可更改文档，但光标可以上下左右移动

b. 输入的字符添加在光标前

c. 若要在原有文本内容的下面追加内容，在命令模式中敲击o键进入输入模式更会高效
{% endhint %}

**Step3.** 停止输入模式（编辑），进入末行模式

Esc

**Step4.** 末行模式，退出文件，返回Linux

`:q!`

`:wq!`

**Step5.** 查看

`cat <file_name>`

{% hint style="info" %}
保存在哪里了？
{% endhint %}







#### Refenrences

https://www.linuxprobe.com/chapter-04.html




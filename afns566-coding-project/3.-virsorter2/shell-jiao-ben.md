---
description: difficulty level ⭐️ ⭐️⭐️
---

# 3.2 Shell

#### 3.2.1 Introduction

1\) The bash shell

**Shell** provides an interface between the user and the kernel \(The core of Linux operating system\).

**Bash** is the shell, or command language interpreter, for the Linux operating system. 

```text
(base) [nanzhen@admin ~]$ echo $SHELL
>>> /bin/bash

#all upper-case variables are set by bash.

(base) [nanzhen@admin ~]$ echo $BASH_VERSION
>>> 4.2.46(2)-release
```

2\) Shell scripting

A **shell script** is a text file containing a sequence of commands, so it tells the shell to execute those commands instead of entering the commands line by line.

**Shell keywords** such as if..else, do..while. **Shell commands** such as pwd, test, echo, continue, type. 

#### 3.2.2 Variables in shell

Variables are used to store data and configuration options. There are two types of variable, **user defined variables** and **system variables**.

{% tabs %}
{% tab title="System Variables" %}
To see all system variables, type `set` or `env` at the terminal.
{% endtab %}

{% tab title="User Defined Variables" %}
Use `varName=someValue` to assign values to shell variables.

Then, run `echo "$varName"` or `echo "${varName}"` to display the value of a variable.

If you know what the variable contains, you can run `echo $varName`.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**DO NOT** put spaces on either side of the equal sign when assigning value to variable.
{% endhint %}

#### 3.2.3 Start up simple scripts

**Step 1.** Run `vim practice_bash.sh` to create a .sh file.

**Step 2.** Type contents below in vim.

```text
#!/bin/bash
#add some comments here. they will be ignored.
pwd
ls -al
~                                                                                                                   
~  
~                                                                                                                 
    
```

The **\#! syntax** used in scripts to indicate an interpreter for execution under Linux operating systems. Most Linux shell and python script starts with `#!/bin/bash` or `#!/usr/bin/python3`. 

A word or line beginning with **\#** causes that word and all remaining characters on that line to be ignored. It helps other system admins to understand your code, logic and it helps them to modify the script you wrote.

**Step 3.** Close the vim window.

**Step 4.** Run `bash practice_bash.sh` to get the result.

#### 3.2.4 References

* https://www.linuxprobe.com/chapter-04.html
* https://github.com/qinjx/30min\_guides/blob/master/shell.md
* https://bash.cyberciti.biz/guide/Main\_Page  ⭐️ ⭐️⭐️
* https://linuxcommand.org/lc3\_writing\_shell\_scripts.php ⭐️ ⭐️⭐️
* https://www.tutorialspoint.com/unix/unix-using-variables.htm ⭐️ ⭐️⭐️


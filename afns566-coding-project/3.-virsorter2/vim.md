# 3.1 Vim

#### 1.1 Introduction

Vim is a highly configurable text editor built to make creating and changing any kind of text very efficient.

#### 1.2 Get started with Vim

**Step1**. Run `vim practice_vim.txt` to create a .txt file.

So, you open a console window.

**Step2.** Press the I key to get into the Insert Mode.

Three Vim modes are often used.

{% hint style="info" %}
1. Normal mode. It's a default mode, used for navigation and simple editing.
2. Insert mode. It's used for explicitly inserting and modifying text. **Press I or O or A key** to get into it. In the lower-left, you should see -- INSERT --. This means you are in Insert mode.
3. Command line mode. It's used for operations like saving, exiting, etc. **Hit the Esc key** to get into it.
{% endhint %}

**Step3.** Type any content you want in Vim.

```text
a
bb
ccc
dddd
```

**Step4.** Hit the Esc key to get into the command line mode.

**Step5.** Type `:wq!` to close the console window.

`:q!`, forced to close the window and not save modifications.

`:wq!`, forced to close the window and save modifications.

**Step6.** Run `cat <file_name>`to check modifications.

```text
(base) [nanzhen@admin ~]$ vim practice_vim.txt
(base) [nanzhen@admin ~]$ cat practice_vim.txt
a
bb
ccc
dddd
(base) [nanzhen@admin ~]$ 
```

{% hint style="info" %}
保存在哪里了？
{% endhint %}

#### 1.3 Vim cheatsheet

{% file src="../../.gitbook/assets/vim-cheatsheet.pdf" caption="Vim\_cheatsheet" %}

#### 1.4 References

* https://opensource.com/article/19/3/getting-started-vim
* https://www.linuxprobe.com/chapter-04.html






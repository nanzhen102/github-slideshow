# 2. genomes download

#### 2.1 run python interpreter in Linux terminal

to entry python, run `python`

```text
(base) [nanzhen@admin ~]$ python
Python 3.8.3 (default, May 19 2020, 18:47:26) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> conda python
```

{% hint style="info" %}
🧙♂

In python,  type `help` to get more information.

In Linux, type `virsorter --help` to get more information.
{% endhint %}

to exit python, run `quit()` or press Ctrl + D.

```text
>>> quit
Use quit() or Ctrl-D (i.e. EOF) to exit
>>> quit()
(base) [nanzhen@admin ~]$ 
```

to write a python script, use Vim text editor in Linux, copy and paste `#!/usr/bin/env python3` and `# -*- coding: utf-8 -*-` in the .py file.

to execute the python script, run `cd` to navigate the terminal to the directory where the script is located, then run `python name.py` in the terminal.

#### 2.2 learn how to parse website data

move on to [3. Bilibili course-parse website data](3.-bilibili-course.md)

#### 2.3 learn Yangjie's python script

* [ ] re-run the python script and discuss with Yangjie
* [ ] python's os module, use [link1](https://stackabuse.com/introduction-to-python-os-module/), [link2](https://www.runoob.com/python/python-os-path.html)
* [ ] python's csv module, use [this link](https://www.geeksforgeeks.org/working-csv-files-python/)

#### 2.4 re-run Yangjie's script and find where errors are

~~`import urllib`~~ , now, `import urllib.request` , succeed.

use AC number script.

#### 2.5 run python script on lab server

on my laptop, shows " no wegt", why?

so, run it on lab server. succeed.











> 🧙♂ ❓ 
>
> find difference and why
>
> if you run `cd` to another folder
>
> ```text
> (base) [nanzhen@admin ~]$ 
> (base) [nanzhen@admin qnz]$ 
> ```

> 给形参指定默认值时，等号两边不要有空格
>
> `def function_name(parameter_0, parameter_1='default value')`















#### References

https://blog.csdn.net/qq\_28267025/article/details/60337293

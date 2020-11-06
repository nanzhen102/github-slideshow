# \*Notes

#### IndentationError:expected an indented block

find the specific line, press the key Tab

#### SyntaxError: invalid syntax

def command, **DO NOT forget the ":"**

#### 查找目录，如sqlite3的安装

terminal, `which sqlite3` 

#### Linux开头的命令行变成了以“&gt;”开头，不是$了

这说明你上一句命令没有打完，或者是不小心打错了。在一句命令的结尾打\就会出现你说的情况，这时可以接着将命令打完，对于一些很长的命令，用这种方法来进行折行！ 解决方法： 1.直接回车 2.Ctrl+C

#### python3中sqlite3安装出现问题

参考 https://blog.csdn.net/jeryjeryjery/article/details/81707023。已经成功解决

#### AttributeError: module 'urllib' has no attribute 'request'

把`import urllib` 改为`import urllib.request` 

#### What's def\(\)? how to understand it?

```python
def getHtml(url):
# 定义一个函数getHtml。函数就是个你招来的工人，你给他材料，告诉他材料如何拼装，然后工人函数把拼装好的成品给你。
# 材料就是形参。拼装方法就是函数体代码。成品就是函数的输出。
# ()内添加url，为【形参】。再赋予值给url，让函数接受你给url指定的任何值
	page = urllib.request.urlopen(url)
	html = page.read()

	return html
# 最后return告诉工人，你想要的是拼装好的部分材料还是整个拼装好的成品。

# 调用函数getHtml，括号里赋予值给url【形参】，这个赋予的网址，为【实参】。
print(getHtml("https://app.gitbook.com/@nanzhen-qiao/s/afns566-coding-project/for-phd-research/2.-genomes-download"))
```





#### 自己经常出现的错误：

单词拼写错误，最好复制粘贴防止错误

空格丢失，写之前先把两边空格加上




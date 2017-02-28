#Beautiful Soup 文档
Beautiful Soup是一个用来从<font color=#0099ff>HTML</font>和<font color=#0099ff>XML</font>提取数据的<font color=#0099ff>Python</font>库。
它能根据你喜欢的提取器来提供你惯用的方式取导航，搜索和修改文档树。
它通常能节省程序员数小时或者数天的工作时间。

这个文档介绍了<font color=#0099ff>Beautiful Soup 4</font>的所有特性，通过一些简单的例子我会展示给你这个库擅长与什么、它怎么工作、怎么使用它、怎么用它来得到你想要的，和当结果出错的时候要怎么做。

该文档的例子在 Python2.7 和 Python3.2 都应能正常运行。

你可能在寻找<font color=#0099ff>Beautiful Soup 3</font>的文档。如果是这样的话，你应该要知道<font color=#0099ff>Beautiful Soup 3</font>已经不再更新了，在所有新的项目都应该使用<font color=#0099ff>Beautiful Soup 4</font>。如果你想学习<font color=#0099ff>Beautiful Soup 3</font>和<font color=#0099ff>Beautiful Soup 4</font>的不同，请看[移植到BS4](http://www.crummy.com/software/BeautifulSoup/bs4/doc/index.html#porting-code-to-bs4 "移植代码到BS4")。
***
#获得帮助
如果你有一些关于<font color=#0099ff>Beautiful Soup</font>的问题，或者在使用<font color=#0099ff>Beautiful Soup</font>的时候出现问题，<font color=#0099ff>发送邮件去讨论组</font>。如果你的问题涉及到解析HTML文件，请确保要提及到HTML文件里的<font color="red">诊断函数返回的内容</font>
***
#快速开始
这是一个HTML文档，它将会被多次用作例子。这是*Alice in Wonderland*故事中的一部分内容：

    html_doc = """
    <html><head><title>The Dormouse's story</title></head>
    <body>
    <p class="title"><b>The Dormouse's story</b></p>
    
    <p class="story">Once upon a time there were three little sisters; and their names were
    <a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
    <a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
    <a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
    and they lived at the bottom of a well.</p>
    
    <p class="story">...</p>
    """
    
使用<font color=#0099ff>Beautiful Soup</font>解析“三姐妹”的文档，我们得到了一个嵌套数据结构的**BeautifulSoup**对象：

    from bs4 import BeautifulSoup
    soup = BeautifulSoup(html_doc, 'html.parser')
    
    print(soup.prettify())
    # <html>
    #  <head>
    #   <title>
    #    The Dormouse's story
    #   </title>
    #  </head>
    #  <body>
    #   <p class="title">
    #    <b>
    #     The Dormouse's story
    #    </b>
    #   </p>
    #   <p class="story">
    #    Once upon a time there were three little sisters; and their names were
    #    <a class="sister" href="http://example.com/elsie" id="link1">
    #     Elsie
    #    </a>
    #    ,
    #    <a class="sister" href="http://example.com/lacie" id="link2">
    #     Lacie
    #    </a>
    #    and
    #    <a class="sister" href="http://example.com/tillie" id="link2">
    #     Tillie
    #    </a>
    #    ; and they lived at the bottom of a well.
    #   </p>
    #   <p class="story">
    #    ...
    #   </p>
    #  </body>
    # </html>
    
这是一些导航数据结构的简单方法：

    soup.title
    # <title>The Dormouse's story</title>
    
    soup.title.name
    # u'title'
    
    soup.title.string
    # u'The Dormouse's story'
    
    soup.title.parent.name
    # u'head'
    
    soup.p
    # <p class="title"><b>The Dormouse's story</b></p>
    
    soup.p['class']
    # u'title'
    
    soup.a
    # <a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>
    
    soup.find_all('a')
    # [<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>,
    #  <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>,
    #  <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
    
    soup.find(id="link3")
    # <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>
    
一个简单的任务来提取文档里在< a >标签内的所有URL：

    for link in soup.find_all('a'):
        print(link.get('href'))
    # http://example.com/elsie
    # http://example.com/lacie
    # http://example.com/tillie
    
另一个常用的方法用来提取文档里的所有文字内容：

    print(soup.get_text())
    # The Dormouse's story
    #
    # The Dormouse's story
    #
    # Once upon a time there were three little sisters; and their names were
    # Elsie,
    # Lacie and
    # Tillie;
    # and they lived at the bottom of a well.
    #
    # ...
    
以上的这些是不是你想要的？如果是，请继续看。
***
#安装**Beautiful Soup**
如果你在用最新版的Debian或者Ubuntu Linux，你可以用系统安装包管理器下载<font color=#0099ff>Beautiful Soup</font>:

    $ apt-get install python-bs4

<font color=#0099ff>Beautiful Soup</font>通过Pypi发布，所以如果你不能通过系统安装包管理下载，你可以用`easy_install`或者`pip`。这个包的名字是`beautifulsoup4`，Python2和Python3都运行同样的包。

    $ easy_install beautifulsoup4
    $ pip install beautifulsoup4

（`Beautifulsoup`这个包可能不是你想要的，这是以前的主要发布版本，<font color=#0099ff>Beautiful Soup3</font>。很多软件都还在用BS3，所以它依然有效，但是如果你想写新的代码你应该安装`beautifulsoup4`。）

如果你没有安装`easy_install`或者`pip`。你可以下载<font color=#0099ff>Beautiful Soup</font>源码然后通过`setup.py`安装它。

    $ python setup.py install
    
如果所有的方法都无效（太悲催了），<font color=#0099ff>Beautiful Soup</font>的协议允许你将政客库打包进你的项目中。你可以下载压缩包，复制它的`bs4`目录到你的项目代码库中，然后就可以不用安装<font color=#0099ff>Beautiful Soup</font>了。

作者用 Python2.7 和 Python3.2 来开发<font color=#0099ff>Beautiful Soup</font>，但是它仍然应该能运行在最新的版本中。
***
#安装后的问题
<font color=#0099ff>Beautiful Soup</font>用 Python2 打包。当你用 Python3 安装时，它会自动转换成 Python3 的代码。如果你没有安装包，代码就不会被转换。这里同样在 Windows 机器里报告了被安装的错误版本（这句无意义）。

如果抛出了`ImportError`"No module name HTMLParser"，你的问题是你在 Python3 中运行 Python2 版本的代码。

如果抛出了`ImportError`"No module name html.parser"，你的问题是你在 Python2 中运行 Python3 版本的代码。

在两个情况中，最好的解决方法是完全删除安装在你系统里的<font color=#0099ff>Beautiful Soup</font>（包括所有你解压压缩包是创建的目录）然后尝试重新安装一次。

如果抛出了`SyntaxError`"Invalid syntax"在行`ROOT_TAG_NAME = u'[document]'`,你需要转换 Python2 代码到 Python3 代码。你可以在安装是这么做：

    $ python3 setup.py install
    
或者在 bs4 目录下手动运行 Python 的转换脚本：

    $ 2to3-3.2 -w bs4
    
***
#安装解析器
<font color=#0099ff>Beautiful Soup</font>支持 Python 标准库里的 HTML 解析器，但是它同样支持数个第三方的解析器。其中一个是<font color=#0099ff>lxml 解析器</font>。根据你电脑的不同，你可能会通过以下其中一个命令来安装`lxml`：

    $ apt-get install python-lxml
    $ easy_install lxml
    $ pip install lxml
    
另一个可供选择的解析器是纯 python 实现的`html5lib`库，一个想浏览器那样解析 HTML 的库。根据你电脑的不同，你可能会通过以下其中一个命令来安装`html5lib`：

    $ apt-get install python-html5lib
    $ easy_install html5lib
    $ pip install html5lib
    
这是一个概括这几个库的优点和缺点的表格：

<table class="docutils" border="1">
<colgroup>
<col width="18%">
<col width="35%">
<col width="26%">
<col width="21%">
</colgroup>
<tbody valign="top">
<tr class="row-odd"><td>解析器</td>
<td>使用方法</td>
<td>优点</td>
<td>缺点</td>
</tr>
<tr class="row-even"><td>html.parser</td>
<td><tt class="docutils literal"><span class="pre">BeautifulSoup(markup,</span> <span class="pre">"html.parser")</span></tt></td>
<td><ul class="first last simple">
<li>内置的库</li>
<li>速度适中</li>
<li>文档容错能力强 (在 Python 2.7.3
和 3.2中)</li>
</ul>
</td>
<td><ul class="first last simple">
<li>容错能力弱
(在 Python 2.7.3
和 3.2之前)</li>
</ul>
</td>
</tr>
<tr class="row-odd"><td>lxml HTML 解析器</td>
<td><tt class="docutils literal"><span class="pre">BeautifulSoup(markup,</span> <span class="pre">"lxml")</span></tt></td>
<td><ul class="first last simple">
<li>速度很快</li>
<li>容错能力强</li>
</ul>
</td>
<td><ul class="first last simple">
<li>需要安装C语言库</li>
</ul>
</td>
</tr>
<tr class="row-even"><td>lxml XML 解析器</td>
<td><tt class="docutils literal"><span class="pre">BeautifulSoup(markup,</span> <span class="pre">"lxml-xml")</span></tt>
<tt class="docutils literal"><span class="pre">BeautifulSoup(markup,</span> <span class="pre">"xml")</span></tt></td>
<td><ul class="first last simple">
<li>速度很快</li>
<li>唯一支持 XML 的解析器</li>
</ul>
</td>
<td><ul class="first last simple">
<li>需要安装C语言库</li>
</ul>
</td>
</tr>
<tr class="row-odd"><td>html5lib</td>
<td><tt class="docutils literal"><span class="pre">BeautifulSoup(markup,</span> <span class="pre">"html5lib")</span></tt></td>
<td><ul class="first last simple">
<li>最强的容错性</li>
<li>跟浏览器一样的解析方式</li>
<li>创建 HTML5 格式的文档</li>
</ul>
</td>
<td><ul class="first last simple">
<li>速度很慢</li>
<li>只支持 Python</li>
</ul>
</td>
</tr>
</tbody>
</table>

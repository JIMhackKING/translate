###首先附上 requests 库的英文文档
[http://docs.python-requests.org/en/master/](http://docs.python-requests.org/en/master/)
#Requests:给人类使用的HTTP库
发行版本：2.13.0
[安装说明](http://docs.python-requests.org/zh_CN/latest/user/install.html#install "安装说明")

**Requests**是唯一一个非转基因的 Python HTTP 库，人类可以安全享用。

注意：用其他HTTP库可能会有危险的副作用，

包括：安全漏洞，冗杂的代码，重复造轮子，不断地查看文档，抑郁沮丧，头痛，甚至死亡。（太狂妄了）
***
##看，Requests的力量：
    >>> r = requests.get('https://api.github.com/user', auth=('user', 'pass'))
    >>> r.status_code
    200
    >>> r.headers['content-type']
    'application/json; charset=utf8'
    >>> r.encoding
    'utf-8'
    >>> r.text
    u'{"type":"User"...'
    >>> r.json()
    {u'private_gists': 419, u'total_private_repos': 77, ...}
阅读[未使用Requests的相似代码](https://gist.github.com/973705)

**Requests**允许你发送天然有机的 *HTTP/1.1*请求，不需要手动的工作。这不需要手动添加查询字符串到你的URL中，或者提交数据到POST中。保持链接和HTTP连接池是完全自动的，由内嵌在Requests内的[urllib3](https://github.com/shazow/urllib3)提供技术支持。
##用户评价
女王殿下的政府、亚马逊、谷歌、Twilio、Runscope、Mozilla、Heroku、Paypal,NPR、美国的奥巴马、Transifex、Native Instruments、Washington Post、Twitter、SoundCloud、Kippt、Readability、以及若干不愿公开身份的美国联邦机构的内部人员。
###Armin Ronacher—
>Requests 是一个完美API，它可以用正确的抽象等级取工作。
###Matt Deboard—
>我要想个办法，把 @kennethreitz 写的 Python requests 模块做成纹身。一字不漏。
###Daniel Greenfeld
>感谢 @kennethreitz 的 Requests 库，刚刚用 10 行代码炸掉了 1200 行意大利面代码。今天真是爽呆了！
###Kenny Meyers
>Python HTTP: 疑惑与否，都去用 Requests 吧。简单优美，而且符合 Python 风格。
##功能特性
Requests 已经为现在的web准备着

- 保持连接和连接池
- 国际化域名和URL
- 持续的Cookie会话
- 像浏览器那样的SSL验证
- 内容自动解码
- 基本/摘要式的身份验证
- 优雅的键值对风格的Cookies
- 自动解压
- Unicode 响应文本
- 支持HTTP(S)代理
- 多部分的文件上传
- 流式下载
- 连接超时
- 分块请求
- 支持 .netrc
- 安全的多线程

Requests正式支持 Python 2.6-2.7 和 3.3-3.7，也在PyPy上有良好支持。
##用户指南
文档的最多单一文章的这一部分，从一些关于Requests的背景信息开始，然后一步一步的介绍Requests库。

- [介绍](http://docs.python-requests.org/zh_CN/latest/user/intro.html)
- - [哲学](http://docs.python-requests.org/zh_CN/latest/user/intro.html#id2)
- - [Apache2许可](http://docs.python-requests.org/zh_CN/latest/user/intro.html#apache2)
- - [Requests许可](http://docs.python-requests.org/zh_CN/latest/user/intro.html#requests)
- [安装](http://docs.python-requests.org/zh_CN/latest/user/install.html)
- - [Pip Install Requests](http://docs.python-requests.org/zh_CN/latest/user/install.html#pip-install-requests)
- - [获取源代码](http://docs.python-requests.org/zh_CN/latest/user/install.html#id2)
- [快速开始](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html)
- - [进行请求](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html#id2)
- - [传如参数进URL](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html#url)
- - [响应内容](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html#id3)
- - [二进制响应内容](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html#id4)
- - [JSON响应内容](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html#json)
- - [原始响应内容](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html#id5)
- - [定制请求头](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html#id6)
- - [更多复杂的POST请求](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html#post)

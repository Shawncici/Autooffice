# Requests库
爬虫采用requests库进行http请求
Requests库暗黄方法为
pip install requests
其用法包括
·re.status_code 响应的HTTP状态码——若返回为200 ，则表示请求成功
·re.text 响应内容的字符串形式——返回的是服务器相应内容的字符串形式，也就是文本内容。主要用于获取文本内容
·rs.content 响应内容的二进制形式——主要用于图片、视频、音频等内容的获取和下载
·rs.encoding 响应内容的编码——爬取内容的编码形似，常见的编码方式有ASCII、GBK、UTF-8等，如果用与文件不同的方式去解码，就会得到一堆乱码。

例如，获取某张图片
import requests
# 发出http请求
#下载图片
res=requests.get('https://img-blog.csdnimg.cn/20210424184053989.PNG')
# 以二进制写入的方式打开一个名为 info.jpg 的文件
with open('datawhale.png','wb') as ff:
    # 将数据的二进制形式写入文件中
    ff.write(res.content)

     
## HTML解析与提取
# 浏览器工作原理
向浏览器中输入某个网址，浏览器会向服务器发出请求，然后服务器做出响应。服务器返回给浏览器的结果就是HTML代码，浏览器会根据HTML代码将网页解析成平时看到的样子

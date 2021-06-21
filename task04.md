# python与PDF

python操作pdf主要涉及到的库PyPDF2
导入模块的方法为
from PyPDF2 import PdfFileReader, PdfFileWriter
其中：
PdfFileReader 可以理解为读取器
PdfFileWriter可以理解为写入器

## 加密
加密很简单，只需要记住：「加密是针对写入器加密」
因此只需要在相关操作完成后调用pdf_writer.encrypt(密码)
以单个PDF的加密为例：
https://mmbiz.qpic.cn/mmbiz_png/2GcSFhuAFlCqbUMweVHHyjQmbCztYEGmtEnib1HIjNvJ65Wapictz3cPZhWTlUhGkjrT2ib7KgIkaTsjiciankYKdrg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1![image](https://user-images.githubusercontent.com/33819026/122712498-957f3000-d296-11eb-9c5d-144b9a0c01fb.png)

## 拆分pdf
拆分的逻辑是：
  读取器读取PDF文档
  读取器一页一页交给写入器
  写入器每获取一页就立即输出
因此，写入器初始化和输出的位置一定都在读取PDF循环每一页的循环体内，而不是在循环体外。
![image](https://user-images.githubusercontent.com/33819026/122712603-c1021a80-d296-11eb-9a83-51281c339ff5.png)

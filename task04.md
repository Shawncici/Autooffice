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
![image](https://user-images.githubusercontent.com/33819026/122712700-eabb4180-d296-11eb-919a-3279809e43ed.png)


## 拆分pdf
拆分的逻辑是：
  读取器读取PDF文档
  读取器一页一页交给写入器
  写入器每获取一页就立即输出
因此，写入器初始化和输出的位置一定都在读取PDF循环每一页的循环体内，而不是在循环体外。
![image](https://user-images.githubusercontent.com/33819026/122712603-c1021a80-d296-11eb-9a83-51281c339ff5.png)


## 合并PDF
逻辑如下：
读取器将所有pdf读取一遍
读取器将读取的内容交给写入器
写入器统一输出到一个新pdf
这里还有一个重要的知识点：读取器只能将读取的内容一页一页交给写入器。
因此，逻辑中第1步和第2步实际上不是彼此独立的步骤，而是读取器读取完一个pdf后，就将这个pdf全部页循环一遍，挨页交给写入器。最后等读取工作全部结束后再输出。
看一下代码可以让思路更清楚：
![image](https://user-images.githubusercontent.com/33819026/122712742-00306b80-d297-11eb-925f-24687c9b59fd.png)

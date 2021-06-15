# 办公自动化学习笔记- task01

## 1 读写文件

### 1.1 读取文件内容

read() 读取文件内容

readlines() 按行进行读取文件中的内容，取得一个字符串列表，列表中每个字符串是文本中的一行，且\n 结束。

```python
helloFile=open('helloFile.txt')
hellocontent= helloFile.read()

sonnetFile=open('D:\\Datawhale\\python办公自动化\\hello.txt')
sonnetFile.readlines()
```

### 1.2 写入文件

写模式：w ，此时将覆盖原有的文件，从头开始；

添加模式：a， 将在原有文件的末尾添加文本

`baconFile=open('bacon.txt','w')`

当写入结束后，需要关闭文件，才能在文件中看到写入的内容

`如 baconFile.close()`

### 1.3 shutil 模块实现复制、移动、重命名等功能

**复制文件和文件夹**

`shutil.copy(source, destination) `

含义是：将路径source处的文件复制到路径destination处 的文件夹，并返回新复制文件绝对路径字符串

**文件和文件夹的移动和改名**

`shutil.move(source, destination) `

含义是：：将路径 source 处的文件/文件夹移动到路径destination，并 返回新位置的绝对路径的字符串。

### 1.4 遍历目录树

`os.walk(path)` :传入一个文件夹的路径，在for循环语句中使用 os.walk() 函数，遍历目录树，和 range()函数遍历一个范围的数字类似。

但`os.walk(path)`会在循环的每次迭代中，返回三个数值：

 1）当前文件夹名称的字符串

 2）当前文件夹中子文件夹的字符串的列表。

 3）当前文件夹中文件的字符串的列表。



## 2 自动发送邮件

python内置库：`smtplib` 和 `email`实现邮件功能，

其中

`smtplib`库负责发送邮件，`email`库负责构造邮件格式和内容；

``````python
#导入相关库
import smtplib #导入库
from smtplib import SMTP_SSL #加密邮件内容，防止中途被截获
from email.mime.text import MIMEText #构造邮件的正文
from email.mime.image import MIMEImage #构造邮件的图片
from email.mime.multipart import MIMEMultipart #把邮件的各个部分装在一起，邮件的主体
from email.header import Header #邮件的文件头，标题，收件人

#设置邮箱域名、发件人邮箱、邮箱授权码、收件人邮箱
host_server = 'smtp.163.com' #sina 邮箱smtp服务器 #smtp 服务器的地址
sender_163 = 'pythonauto_emai@163.com' #sender_163为发件人的邮箱
pwd = 'DYEPOGLZDZYLOMRI' #pwd为邮箱的授权码'DYEPOGLZDZYLOMRI'
#也可以自己注册个邮箱，邮箱授权码'DYEPOGLZDZYLOMRI' 获取方式可参考
#http://help.163.com/14/0923/22/A6S1FMJD00754KNP.html
receiver = '********@163.com'

#3 构建MIMEMultipart对象代表邮件本身，可以往里面添加文本、图片、附件等
msg = MIMEMultipart() #邮件主体
#4 设置邮件头部内容
mail_title = 'python办公自动化邮件' # 邮件标题
msg["Subject"] = Header(mail_title,'utf-8') #装入主体
msg["From"] = sender_163 #寄件人
msg["To"] = Header("测试邮箱",'utf-8') #标题
#5 添加正文文本
mail_content = "您好，这是使用python登录163邮箱发送邮件的测试" #邮件的正文内容
message_text = MIMEText(mail_content,'plain','utf-8') #构造文本,参数1：正文内容，参
数2：文本格式，参数3：编码方式
msg.attach(message_text) # 向MIMEMultipart对象中添加文本对象
#6 添加图片
image_data = open('cat.jpg','rb') # 二进制读取图片
message_image = MIMEImage(image_data.read()) # 设置读取获取的二进制数据
image_data.close() # 关闭刚才打开的文件
msg.attach(message_image) # 添加图片文件到邮件信息当中去
# 7 添加附件(excel表格)
atta = MIMEText(open('cat.xlsx', 'rb').read(), 'base64', 'utf-8') # 构造附件
atta["Content-Disposition"] = 'attachment; filename="cat.xlsx"' # 设置附件信息
msg.attach(atta) ## 添加附件到邮件信息当中去
#8 发送邮件
smtp = SMTP_SSL(host_server) #SSL登录 创建SMTP对象
smtp.login(sender_163,pwd) ## 登录邮箱，传递参数1：邮箱地址，参数2：邮箱授权码
smtp.sendmail(sender_163,receiver,msg.as_string()) # 发送邮件，传递参数1：发件人邮箱地
址，参数2：收件人邮箱地址，参数3：把邮件内容格式改为str
print("邮件发送成功")
smtp.quit # 关闭SMTP对象

### 库
python处理word需要用到的库为 python-docx库
pip3 install python-docx

### docx库处理word的原理
python-docx 将整个文章看做是一个 Document 对象 ，其基本结构如下：
每个 Document 包含许多个代表“段落”的 Paragraph 对象，存放在 document.paragraphs 中。
每个 Paragraph 都有许多个代表"行内元素"的 Run 对象，存放在 paragraph.runs 中。
在 python-docx 中， run 是最基本的单位，每个 run 对象内的文本样式都是一致的，也就是说，在从
docx 文件生成文档对象时， python-docx 会根据样式的变化来将文本切分为一个个的 Run 对象。


### 创建或打开 Document
Python-docx 导入包时是以 docx 命令存在的，与 Opencv 的 Python 版本导入方法相似；创建文件、打开文件以 Document() 命令操作，这里操作时需要注意几个点：
1）Document() 命令是基于默认”模板“创建一个空白文档，随后可对文档进行编辑操作，最后没有用 save() 函数存储的话，文档将伴随程序结束同内存一起
2）Document(path) 命令表示打开一个本地已经存在的 docx 文件，path 表示存放目录若不存在则程序报错；


### 加入一段落
段落作为 docx 文档正文的主要成分，那怎样在创建好的 Document 中加入一段话呢？官方给出了两种方式

1）在文档后面插入
这种方法是比较常见且简单的，命令如下
paragraph = document.add_paragraph('Lorem ipsum dolor sit amet.')
方法中将创建好的段落引用指向 paragraph ，表明了光标的位置，后面的一些操作可以借助 paragraph 引用变量来作为定位操作

2）在指定地方的前面插入
文档编辑正常顺序是在末尾进行编辑，但有时在编辑时可能失误少输入一段话或文字，这时就用到 在指定位置前面 进行插入操作
prior_paragraph = paragraph.insert_paragraph_before('Lorem ipsum')
此命令常用于 修正文档 ，当需要在一段话前面添加一些别的文字时。

### 标题
docx 中 会用一、二、三级标题将正文分为几部分，让文本主次感更强；Python-docx 有对应的内置函数供我们使用，内置函数中标题分为主标题和子标题
创建标题的函数方法中，有一个参数 level 可进行修改，若不设定时默认为 主标题（leve = 0）；
document.add_heading('The REAL meaning of the universe')
子标题分为 1-9 九个等级，修改参数 level 即可
document.add_heading('The role of dolphins', level=2)

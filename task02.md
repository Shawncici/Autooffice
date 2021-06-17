## Excel读取、写入
读取、写入对应表格需要用到openpyxl库

安装： pip install openpyxl

导入：from openpyxl import Workbook

## 打开文件
1. 创建文件
from openpyxl import Workbook 
# 实例化
wb = Workbook()
# 激活 worksheet
ws = wb.active

2.打开已有的文件
>>> from openpyxl import load_workbook
>>> wb2 = load_workbook('文件名称.xlsx')

3.存储数据
# 方式一：数据可以直接分配到单元格中(可以输入公式)
ws['A1'] = 42
# 方式二：可以附加行，从第一列开始附加(从最下方空白处，最左开始)(可以输入多行)
ws.append([1, 2, 3])
# 方式三：Python 类型会被自动转换
ws['A3'] = datetime.datetime.now().strftime("%Y-%m-%d")

4.创建表（sheet）
# 方式一：插入到最后(default)
>>> ws1 = wb.create_sheet("Mysheet") 
# 方式二：插入到最开始的位置
>>> ws2 = wb.create_sheet("Mysheet", 0)

5.选择表（sheet）
# sheet 名称可以作为 key 进行索引
>>> ws3 = wb["New Title"]
>>> ws4 = wb.get_sheet_by_name("New Title")
>>> ws is ws3 is ws4
True

6.查看表名（sheet）
# 显示所有表名
>>> print(wb.sheetnames)
['Sheet2', 'New Title', 'Sheet1']
# 遍历所有表
>>> for sheet in wb:
... print(sheet.title)

7.访问单元格（call）
# 方法一
>>> c = ws['A4']
# 方法二：row 行；column 列
>>> d = ws.cell(row=4, column=2, value=10)
# 方法三：只要访问就创建
>>> for i in range(1,101):
...     for j in range(1,101):
...      ws.cell(row=i, column=j)

8.保存数据
>>> wb.save('文件名称.xlsx')



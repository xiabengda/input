> 实现对 后缀名为 .csv文件的 读写操作
## 概述

CSV (Comma Separated Values) 格式是电子表格和数据库中最常见的输入、输出文件格式。

CSV纯文本，使用某种字符集（ASCII，Unicode，GB2312等）

CSV 文件中的每一行都是一个数据记录。 每条记录都有相同的字段序列。每个记录由一个或多个字段组成，用逗号分隔。或者用"|"，分号，制表符等等

csv 模块中的 **reader** 类和 **writer** 类可用于读写序列化的数据。也可使用 **DictReader** 类和 **DictWriter** 类以字典的形式读写数据。
## 内容
### 方法

> reader()


### 对象
## 问题

### writerrow写入时有空行？
在打开文件的方法里面设置参数：newline=‘’   即可
```python
import csv
 
with open('data.csv','w',newline='') as file:
    writer = csv.writer(file)
    writer.writerow(['id','name','age'])
    writer.writerow(['10001','ZhangSan',18])
    writer.writerow(['10002','LiSi','20'])
```
### 使用UTF-8写入CSV中文乱码
使用encoding=‘utf-8’，写入的文档是乱码：

```python
def save_contents(urlist):
    with open("filename"+".csv","a+",newline='', encoding='utf-8') as f:
        writer = csv.writer(f)
        for i in range(len(urlist)):
            writer.writerow(urlist[i])
```

解决方法：修改 encoding=‘utf-8-sig’：

```python
def save_contents(urlist):
    with open("filename"+".csv","a+",newline='', encoding='utf-8-sig') as f:
        writer = csv.writer(f)
        for i in range(len(urlist)):
            writer.writerow(urlist[i])
```
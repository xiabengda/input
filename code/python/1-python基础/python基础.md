- python基础
	- print
	- 注释
	- 变量
	- 运算符
		- 内容
			- 逻辑：not/and/or
		- 优先级
	- 数据类型
		- 内容
			- 字符串
			- 整数
			- 浮点数
			- 布尔型
			- None
			- 列表
				- 格式
				- 方法
					- 增删改查
					- 最值
					- 排序
			- 字典
			- 元组：不可变
		- 转置
			- str/int/float...
			- 我
	- 函数
		- 内置函数
			- type
			- len
			- input
			- range
			- 字符串{变量1}{变量2}.format(变量1，变量2)/f"字符串{变量}"
		- 自定义函数
	- 条件/循环
		- 条件
			- 语法
		- 循环：for/while
	- 模块
		- 使用模块
			- import/from...import...
			- 安装第三方库：pip install 库名
		- 常用模块
			- pandas
			- 
	- 面向对象
		- 封装
		- 继承
		- 多态
	- 操作文件
## print
## 变量
命名一般使用下划线命名法
## 运算符
## 数据类型
### 字符串
## 函数
### 内置函数
### 自定义函数
## 注释
## 条件/循环语句
## 模块
### 函数库--库（外部导入）
import math
math.函数名(...)
## 面向对象
### 封装
### 继承
```python
class Father:  
    def __init__(self, name, sex):  
        self.name = name  
        self.sex = sex  
        self.num_eyes = 2  
  
    def breathe(self):  
        print(self.name + "呼吸...")  
  
    def poop(self):  
        print(self.name + "在拉屎...")    
  
  
class Child1(Father):  
    def __init__(self,name, sex):  
        super().__init__(name, sex)  
        self.has_tail = False  
  
    def grade(self):  
        print(self.name + "小学")    
  
c = Child1('John','male')  
print(c.name)
```
语法：

继承属性：

继承方法--重写：
### 多态
## 操作文件
### 读取文件
语法：打开文件，返回文件对象：`f = open('文件路径','r',encoding='utf-8')`

读取内容：read()，`f.read()`，返回全部文件内容的字符串
```python
f = open(file,'r',encoding='utf-8')  
print(f.read()) # 不要读大文件，会占满内存  
print('----------')  
print(f.read()) # 再次打印会返回空，因为上一次已经读到文件末尾

# print(f.read(10)) # 读取多少字节  
# print('----------')  
# print(f.read()) # 会接着上次读
```
按行读取：`readline()`，返回一行文件内容的字符串
```python
f = open(file,'r',encoding='utf-8') 
print(f.readline())  # 读一行  
line = f.readline() # 读第一行  
while line != "": # 判断当前行是否为空  
    print(line) # 不为空则打印当前行  
    line = f.readline() # 继续读取下一行
```
一次读取所有行：`readlines()`，返回全部文件内容组成列表
```python
f = open(file,'r',encoding='utf-8') 
lines = f.readlines()  
for line in lines:  
    print(line)
```
关闭文件：`f.close()`，关闭文件，释放资源

更加简洁的写法：
```python
# 文件会自动关闭  
with open(file,'r',encoding='utf-8') as f:  
    print(f.read())
```
### 写入内容
### 模式
- r：只读
- w：只写，会清空之前的内容
- a：追加
- r+：读写，写的时候是追加

## 异常
```python
try:  
    pass  # 有可能产生错误的代码  
except ValueError:  
    print("产生错误值时运行")  
except ZeroDivisionError:  
    print("产生除零错误时运行")  
except:  
    print("产生其他错误时运行")  
else:  
    print("没有错误时运行")  
finally:  
    print("不管是否发生错误都会运行")
```
## 测试
### assert
### unittest
```python
import unittest  
from my_calculator import my_adder  
  
class TestMyAdder(unittest.TestCase): # 创建测试类继承于unittest里面的TestCase类  
    # 创建对象，统一处理  
    def setUp(self):  
        pass  
        # self.duiXiang = className(ddd,ddd,ddd)  
    # 测试用例，必须以test开头  
    def test_positive_with_positive(self):  
        self.assertEquals(my_adder(3, 5), 8)  
  
    def test_negative_with_positive(self):  
        self.assertEquals(my_adder(-3, 5), -1)  
  
# if __name__ == '__main__':  
#     unittest.main()
```
## 正则表达式
### 正则基本语法
概念：一种使用表达式的方式对字符串进行匹配的语法规则

使用元字符进行排列组合来匹配字符串，`每个元字符默认只匹配一位字符`

> **元字符**：具有固定含义的特殊符号
```
.    匹配除换行符以外的任意字符，一个点表示一个字符
\w   匹配字母或数字或下环线
\s   匹配任意的空白符，包括空格，换行，回车
\d   匹配数字
\n   匹配一个换行符
\t   匹配一个制表符

^    匹配字符串的开始，以什么开始
$    匹配字符串的结尾，以什么结尾

\W   匹配非字母或数字或下划线
\S   匹配非空字符
\D   匹配非数字

a|b  匹配字符a或字符b
()   匹配括号内的表达式，也表示一个组
[...]  匹配字符组中的字符，符合中括号里面规则的所有字符
[^...] 匹配除了字符组中字符以外的所有字符
```
举例：
```
[a-zA-Z0-9] #匹配所有字母和所有数字
```
> **量词**：控制前面的元字符出现的次数
```
*       重复零次或更多次
+       重复一次或更多次
?       重复零次或一次
{n}     重复n次
{n,}    重复n次或更多次
{n,m}   重复n到m次
```
举例
```
\d\d\d\d == \d{4}
```
> 贪婪匹配和惰性匹配

```
.*     贪婪匹配
.*?    惰性匹配，?尽可能让*少的去匹配东西
```
举例
```python
str = "玩儿吃鸡游戏，晚上一起上游戏，干嘛呢？打游戏啊"  
  
s = re.compile("玩儿.*?游戏")  
print(s.findall(str)) # ['玩儿吃鸡游戏']
# 玩儿吃鸡游戏 ----.*?尽可能少的匹配，结果是这个
# 玩儿吃鸡游戏，晚上一起上游戏
# 玩儿吃鸡游戏，晚上一起上游戏，干嘛呢？打游戏

str2 = "sakldjxfjieoqiuex"
s2 = re.compile(".*?x")
print(s2.findall(str2)) # ['sakldjx', 'fjieoqiuex']

str: <div>胡辣汤</div>
reg: <.*>
结果：<div>胡辣汤</div>
```
> 分组

```
(ab)    将括号中字符作为一个分组
(?P<name>.*?)    分组起别名，匹配到的字符串在外部是通过定义的name来获取
\Num或者(?P=name) 快捷调用之前的分组内容

ret = re.match(r"<([a-zA-Z]*)>\w*</\1>", "<html>hh</html>")  
print(ret.group()) # <html>hh</html>，这里的\1==([a-zA-Z]*)

ret = re.match(r"<(?P<name1>\w*)><(?P<name2>\w*)>.*</(?P=name2)></(?P=name1)>","<html><h1>www.itcast.cn</h1></html>")  
print(ret.group())

.group("name")   获取分组名为name的内容
```
> flags

标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。

```
re.I    忽略大小写
re.L    表示特殊字符集 \w, \W, \b, \B, \s, \S 依赖于当前环境
re.M    多行模式
re.S    即为 . 并且包括换行符在内的任意字符（. 不包括换行符）
re.U    表示特殊字符集 \w, \W, \b, \B, \d, \D, \s, \S 依赖于 Unicode 字符属性数据库
re.X    为了增加可读性，忽略空格和 # 后面的注释
```

[正则表达式在线测试](https://tool.oschina.net/regex)

### re模块
> 1、findall 匹配字符串中所有符合正则的内容，返回一个列表list

```python
lst = re.findall("m", "mai le fo len, mai ni mei!")  
print(lst)
```
> 2、search 会进行匹配.但是如果匹配到了第一个结果.就会返回这个结果.如果匹配不上search返回的则是None，返回的是match对象，拿数据需要.group()
```python
ret=re.search(r'\d+','5点之前.你要给我5000万').group()
print(ret) # 5
```

>3、match 只能从字符串的开头进行匹配，返回一个match对象，拿数据需要.group()

```python
ret = re.match('a','abc').group()
print(ret) # a
```
> 4、finditer和findall差不多，只不过这时返回的是迭代器（重点），从迭代器中拿内容需要.group()

```python
it = re.finditer("m","mai le fo len,mai ni mei!")
for i in it:
	print(i.group())
```

> 5、complie，预加载正则表达式，方便后面的使用
```python
obj = re.compile(r"\d+")
result = obj.seach(string) == re.seach(pattern, string)
```
> 6、正则中的内容如何单独提取？单独获取到正则中的具体内容可以给分组起名字

(?P<分组名字>正则) 可以单独从正则匹配的内容中进一步提取内容

```python
s = '''  
    <div class='西游记'><span id='10010'>中国联通</span></div>  
'''  
obj = re.compile(r"<span id='(?P<id>\d+)'>(?P<name>\w+)</span>",re.S)  
# re.S：让.能匹配换行符  
result = obj.search(s)  
print(result.group()) # 结果：<span id='10010'>中国联通</span>  
print(result.group("id")) # 结果：10010#获取id组的内容  
print(result.group("name")) # 结果：中国联通 # 获取name组的内容
```


> sub

sub是substitute的所写，表示替换，将匹配到的数据进⾏替换。

语法：re.sub(pattern, repl, string, count=0, flags=0)

- pattern：正则规则
- repl：要替换的字符串，也可以是一个函数
- string：原始字符串
- count：可选参数，_count_ 是要替换的最大次数，必须是非负整数。如果省略这个参数或设为 0，所有的匹配都会被替换
- flag：可选参数，标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。

```python
import re
ret = re.sub(r"\d+", '998', "python = 997")
print(ret) # python = 998
```

```python
import re
def add(temp):
    #int（）参数必须是字符串，类似字节的对象或数字，而不是“re.Match”
    strNum = temp.group()
    num = int(strNum) + 1
    return str(num)
ret = re.sub(r"\d+", add, "python = 997")
print(ret)
ret = re.sub(r"\d+", add, "python = 99")
print(ret)
```

> subn

行为与`sub()`相同，但是返回一个元组 `(字符串, 替换次数)`。

> split

功能： 以正则表达式切割字符串  

返回值 ： 分割后的内容放入列表
```python
l = re.split(r'\s+','hello python')
print(l)
```
### 贪婪与非贪婪

## 多线程
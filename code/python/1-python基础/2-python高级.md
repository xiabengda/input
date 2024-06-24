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
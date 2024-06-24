# Flask学习笔记

## 1、安装

## 2、路由

## 4、模板

> 1、概念：

模板中的变量是一种占位符 告诉模板该位置的值是从渲染是的哪个数据中获取出来的

> 2、设置

> **3、语法**

- 1、在试图函数中，渲染模板的过程中添加数据

```python
return render_template('index.html',变量1=值1,变量2=值2)
```

- 2、在模板中，获取变量的值放到指定位置**（数据交互）**

```python
@app.route('/')
def index():
    return render_template('index.html',
                           book='<<钢铁是怎样练成的>>',
                           author='奥斯特洛夫斯基',
                           rice=32.5,
                           editor='北京大学出版社'
                           )
```

```html
<div class="container">
        主要内容
        <p>书名：{{book}}</p>
        <p>作者：{{author}}</p>
        <p>价格：{{rice}}</p>
        <p>出版社：{{editor}}</p>
    </div>
```

- 3、过滤器


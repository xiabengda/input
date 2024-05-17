# console对象与控制台
## console对象
`console`对象是 JavaScript 的原生对象，它有点像 Unix 系统的标准输出`stdout`和标准错误`stderr`，可以输出各种信息到控制台，并且还提供了很多有用的辅助方法。

`console`的常见用途有两个。

- 调试程序，显示网页代码运行时的错误信息。
- 提供了一个命令行接口，用来与网页代码互动。

`console`对象的浏览器实现，包含在浏览器自带的开发工具之中。以 Chrome 浏览器的“开发者工具”（Developer Tools）为例，可以使用下面三种方法的打开它。

1. 按 F12 或者`Control + Shift + i`（PC）/ `Command + Option + i`（Mac）。
2. 浏览器菜单选择“工具/开发者工具”。
3. 在一个页面元素上，打开右键菜单，选择其中的“Inspect Element”。
## console对象的静态方法
`console`对象提供的各种静态方法，用来与控制台窗口互动。
### console.log()，console.info()，console.debug()

`console.log`方法用于在控制台输出信息。它可以接受一个或多个参数，将它们连接起来输出。

`console.log`方法支持以下占位符，不同类型的数据必须使用对应的占位符。
- `%s` 字符串
- `%d` 整数
- `%i` 整数
- `%f` 浮点数
- `%o` 对象的链接
- `%c` CSS 格式字符串

`console.info`是`console.log`方法的别名，用法完全一样。只不过`console.info`方法会在输出信息的前面，加上一个蓝色图标。

`console.debug`方法与`console.log`方法类似，会在控制台输出调试信息。但是，默认情况下，`console.debug`输出的信息不会显示，只有在打开显示级别在`verbose`的情况下，才会显示。

### console.warn()，console.error()

`warn`方法和`error`方法也是在控制台输出信息，它们与`log`方法的不同之处在于，`warn`方法输出信息时，在最前面加一个黄色三角，表示警告；`error`方法输出信息时，在最前面加一个红色的叉，表示出错。同时，还会高亮显示输出文字和错误发生的堆栈。其他方面都一样。

### console.table()

对于某些复合类型的数据，`console.table`方法可以将其转为表格显示。
```js
var languages = [
  { name: "JavaScript", fileExtension: ".js" },
  { name: "TypeScript", fileExtension: ".ts" },
  { name: "CoffeeScript", fileExtension: ".coffee" }
];
console.table(languages);
```
### console.count()

`count`方法用于计数，输出它被调用了多少次。

该方法可以接受一个字符串作为参数，作为标签，对执行次数进行分类。
```js
function greet(user) {
  console.count(user);
  return "hi " + user;
}
greet('bob')
// bob: 1
// "hi bob"
greet('alice')
// alice: 1
// "hi alice"
greet('bob')
// bob: 2
// "hi bob"
```
### console.dir()，console.dirxml()

`dir`方法用来对一个对象进行检查（inspect），并以易于阅读和打印的格式显示。

该方法对于输出 DOM 对象非常有用，因为会显示 DOM 对象的所有属性。

`dirxml`方法主要用于以目录树的形式，显示 DOM 节点。
1. `console.dirxml(document.body)`

如果参数不是 DOM 节点，而是普通的 JavaScript 对象，`console.dirxml`等同于`console.dir`。
### console.assert()

`console.assert`方法主要用于程序运行过程中，进行条件判断，如果不满足条件，就显示一个错误，但不会中断程序执行。这样就相当于提示用户，内部状态不正确。

它接受两个参数，第一个参数是表达式，第二个参数是字符串。只有当第一个参数为`false`，才会提示有错误，在控制台输出第二个参数，否则不会有任何结果。
```js
console.assert(false, '判断条件不成立')
// Assertion failed: 判断条件不成立
// 相当于
try {
  if (!false) {
    throw new Error('判断条件不成立');
  }
} catch(e) {
  console.error(e);
}
```
下面是一个例子，判断子节点的个数是否大于等于500。

1. `console.assert(list.childNodes.length < 500, '节点个数大于等于500')`

上面代码中，如果符合条件的节点小于500个，不会有任何输出；只有大于等于500时，才会在控制台提示错误，并且显示指定文本。
### console.time()，console.timeEnd()

这两个方法用于计时，可以算出一个操作所花费的准确时间。
```js
console.time('Array initialize');
var array= new Array(1000000);
for (var i = array.length - 1; i >= 0; i--) {
  array[i] = new Object();
};
console.timeEnd('Array initialize');
// Array initialize: 1914.481ms
```
### console.group()，console.groupEnd()，console.groupCollapsed()

`console.group`和`console.groupEnd`这两个方法用于将显示的信息分组。它只在输出大量信息时有用，分在一组的信息，可以用鼠标折叠/展开。
### console.trace()，console.clear()

`console.trace`方法显示当前执行的代码在堆栈中的调用路径。

`console.clear`方法用于清除当前控制台的所有输出，将光标回置到第一行。如果用户选中了控制台的“Preserve log”选项，`console.clear`方法将不起作用。
## 控制台命令
## debugger语句
`debugger`语句主要用于除错，作用是设置断点。如果有正在运行的除错工具，程序运行到`debugger`语句时会自动停下。如果没有除错工具，`debugger`语句不会产生任何结果，JavaScript 引擎自动跳过这一句。

Chrome 浏览器中，当代码运行到`debugger`语句时，就会暂停运行，自动打开脚本源码界面。
```js
for(var i = 0; i < 5; i++){
  console.log(i);
  if (i === 2) debugger;
}
```
上面代码打印出0，1，2以后，就会暂停，自动打开源码界面，等待进一步处理。
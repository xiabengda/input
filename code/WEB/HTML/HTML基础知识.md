# HTML
## HTML4
## HTML5
### 什么是HTML5 
HTML5 是新一代的 HTML 标准，2014年10月由万维网联盟（ W3C ）完成标准制定。 

官网地址： 
- W3C 提供： https://www.w3.org/TR/html/index.html 
- WHATWG 提供：https://whatwg-cn.github.io/html/multipage 

HTML5 在狭义上是指新一代的 HTML 标准，在广义上是指：整个前端。
### 优势
1. 针对 JavaScript ，新增了很多可操作的接口。 
2. 新增了一些语义化标签、全局属性。 
3. 新增了多媒体标签，可以很好的替代 flash 。 
4. 更加侧重语义化，对于 SEO 更友好。 
5. 可移植性好，可以大量应用在移动设备上。
### 新增标签
#### 布局

| 标签名     | 语义                                   | 单/双标签 |
| :------ | :----------------------------------- | :---- |
| header  | 整个页面，或部分区域的头部                        | 双     |
| footer  | 整个页面，或部分区域的底部                        | 双     |
| nav     | 导航                                   | 双     |
| article | 文章、帖子、杂志、新闻、博客、评论等。                  | 双     |
| section | 页面中的某段文字，或文章中的某段文字（里面文字通常里面会包含 标题）。  | 双     |
| aside   | 侧边栏                                  | 双     |
| main    | 文档的主要内容 ( WHATWG 没有语义， IE 不支持)，几乎不用。 | 双     |
| hgroup  | 包裹连续的标题，如文章主标题、副标题的组合 （ W3C 将其删除）    | 双     |
关于 article 和 section ：
> 1. artical 里面可以有多个 section 。 
> 2. section 强调的是分段或分块，如果你想将一块内容分成几段的时候，可使用 section 元 素。 
> 3. article 比 section 更强调独立性，一块内容如果比较独立、比较完整，应该使用 article 元素。

#### 状态
1、meter标签

语义：定义已知范围内的标量测量。也被称为 gauge （尺度），双标签，例如：电量、磁盘用量 等。

- 属性
	- high：高值
	- low：低值
	- max：最大值
	- min：最小值
	- optimum：最优值
	- value：当前值

2、progress
#### 列表
#### 文本

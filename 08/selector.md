[TOC]

# CSS选择器详解

CSS可以选择元素并进行美化，CSS选择器就是实现选择的工具，实际上在CSS和HTML之间构建桥梁，实现两者之间的沟通。

## 1. [基本选择器](http://css.doyoe.com/selectors/element/index.htm)

### 1.1 通配选择器

#### 1.1.1 简介

- 通配选择符(Universal Selector)
- **选定所有对象**

#### 1.1.2 语法

```css
/*语法*/
* {
	样式声明
}

/* 选择所有元素 */
* {
	padding: 0;
	margin: 0;
}

/*通配符选择符可以省略*/
*[lang^=en] {
	color: green;
}
*.warning {
	color: red;
}
*#maincontent {
	border: 1px solid blue;
}

/*可以跟命名空间配合使用*/
/* 会匹配ns命名空间下的所有元素 */
ns|* {}
/* 会匹配所有命名空间下的所有元素 */
*|* {}
/* 会匹配所有没有命名空间的元素 */
|* {}
```

#### 1.1.3 注意事项

- 会选择命中文档的所有元素
- 谨慎使用
- 浏览器重置

#### 1.1.4 浏览器重置

统一浏览器的默认样式。[参考网站](https://cssreset.com/)!

- 粗暴重置
- reset.css
- normal.css

### 1.2 元素选择器

#### 1.2.1 简介

- 类型选择符(Type Selector)
- **以文档语言对象类型作为选择符。**

#### 1.2.2 语法

```css
/*语法*/
元素 {
	样式声明
}

/* 匹配命中文档中所有span类型的元素 */
span {
	background-color: DodgerBlue;
	color: #ffffff;
}

/* 一般配合关系选择符一起使用 */
nav a{
	text-decoration: none;
}
```

#### 1.2.3 注意事项

- 除了CSS重置或全局设置里，谨慎单独使用！
- 一般配合关系选择符一起使用！

### 1.3 类选择器

#### 1.3.1 简介

- 类选择符(Class Selector)
- 根据元素的类属性中的内容匹配元素。

#### 1.3.2 语法

```css
/*语法*/
.类名 {
	样式声明
}

/*根据类a、类b来选择元素*/
.a {
	color: #f00;
}
.b {
	font-weight: 700;
}
<div class="a b">给某个div元素定义.a和.b两个类</div>
<div class="a">给某个div元素定义.a和.b两个类</div>
<div class="b">给某个div元素定义.a和.b两个类</div>
/*多类选择符使用*/
.a.b {
	color: #f00;
}
```

#### 1.3.3 注意事项

- 最为常用的选择器之一
- 多种选择器配合使用

### 1.4 ID选择器

#### 1.4.1 简介

- ID选择符(ID Selector)
- 会根据该元素的 ID 属性中的内容匹配元素。

#### 1.4.2 语法

```css
/*语法*/
#id属性值 {
	样式声明
}

/* 匹配ID为subtitle的元素 */
#subtitle {
	font-size: 20px;
}
```

#### 1.4.3 id和class的选择

- 身份证号和体貌特征的区别
- 身份证号精确定位一个，只能一一对应；体貌特征批量定位一些，可以N对N。
- CSS用class，JS用id
- 权重不同，id为100，class为10。
- id还有个专门用途，用作定义锚记（链接到片段时使用）
- 如果需要打破统一，用id

## 2. [属性选择器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Attribute_selectors)

### 2.1 属性列表

| 选择符         | 描述                                                         |
| :------------- | :----------------------------------------------------------- |
| E[att]         | 选择具有att属性的E元素。                                     |
| E[att="val"]   | 选择具有att属性且属性值等于val的E元素。                      |
| E[att~="val"]  | 选择具有att属性且属性值为一用空格分隔的字词列表，其中一个等于val的E元素。 |
| E[att^="val"]  | 选择具有att属性且属性值为以val开头的字符串的E元素。          |
| E[att$="val"]  | 选择具有att属性且属性值为以val结尾的字符串的E元素。          |
| E[att*="val"]  | 选择具有att属性且属性值为包含val的字符串的E元素。            |
| E[att\|="val"] | 选择具有att属性且属性值为以val开头并用连接符"-"分隔的字符串的E元素，如果属性值仅为val，也将被选择。 |

### 2.2 语法

```css
/* 属性选择器 */
/* 选择具有href属性的超链接a */
a[href]{}
/* 选择具有name属性的超链接a */
a[name]{}
/* 选择具有name属性的，class等于top的元素 */
.top[name]{}

/* 比上面的a[name]选择范围更小，优先级更高 */
/* 选择具有name属性的，且属性值等于top的元素 */
a[name="top"]{}

/* 选择具有class属性，并且属性值为一个空格隔开的属性列表，bold是其中之一 */
p[class~="bold"]{}
/* 选择具有lang属性，并且属性值为zh或者zh-开头的p元素 */
p[lang|="zh"]{}

/* 选择具备href属性，属性值为#开头的p元素 */
p[href^="#"]{}
/* 选择具备href属性，属性值为.pdf结束的class包含a元素 */
.a[href$=".pdf"]{}

/* 选择具备href属性，属性值包含example的所有元素 */
[href*="example"]{}

/* 设置链接 */
a {
  color: blue;
}

/* 以 "#" 开头的页面本地链接 */
a[href^="#"] {
  background-color: gold;
}

/* 设置语言 */
/* 将所有包含 `lang` 属性的 <div> 元素的字重设为 bold */
div[lang] {
  font-weight: bold;
}

/* 将所有语言为美国英语的 <div> 元素的文本颜色设为蓝色 */
div[lang~="en-us"] {
  color: blue;
}

/* 将所有语言为葡萄牙语的 <div> 元素的文本颜色设为绿色 */
div[lang="pt"] {
  color: green;
}

/* 将所有语言为中文的 <div> 元素的文本颜色设为红色
   无论是简体中文（zh-CN）还是繁体中文（zh-TW） */
div[lang|="zh"] {
  color: red;
}

/* 将所有 `data-lang` 属性的值为 "zh-TW" 的 <div> 元素的文本颜色设为紫色 */
/* 备注: 和 JS 不同，CSS 可以在不使用双引号的情况下直接使用带连字符的属性名 */ 
div[data-lang="zh-TW"] {
  color: purple;
}

/* 设置列表 */
ol[type="a"] {
  list-style-type: lower-alpha;
  background: red;
}

ol[type="a" s] {
  list-style-type: lower-alpha;
  background: lime;
}

ol[type="A" s] {
  list-style-type: upper-alpha;
  background: lime;
}
```

### 2.3 使用案例


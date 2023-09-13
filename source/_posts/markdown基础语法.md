---
title: markdown基础语法
date: 2023-09-12 20:29:22
tags:
categories: web前端
---

之前写文章做记录都是直接码字，码字虽然方便，但是遇到代码部分就很dan疼，尤其是代码格式化很麻烦，开始用markdown之后就觉得特别方便，简单记录下基础语法。

### 1. 标题

标题主要是通过在文字前边加不同数量的 # 去完成

```shell
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```
<img src="/images/markdown/title.png" />

### 2. 正文内容

正文内容直接去打字写就可以了，需要注意的是如果要另起一段的话，是需要按两次回车的，也就是两段之间需要空一行

### 3. 代码块

代码块内容直接放在两个 中间即可，可以在上边后边加上语言类型，会高亮显示语法

```javascript
this is javascript language
function name(){}
```

### 4. 行内代码

行内代码讲代码写在行内的 `` 中间即可

```shell
行内代码可以直接书写，`this is inline code` 样式
```

行内代码可以直接书写，`this is inline code` 样式

### 5. 有序列表和无序列表

有序列表通过文字前边添加1.2.3.4等即可，二级结构通过前边加空格或tab就可以

无序列表通过文字前边添加 * 或者 - 就可以，二级结构同样的方法

```shell
有序列表: 
1. 第一个
2. 第二个
3. 第三个
  1. 第三点的第一个
  2. 第三点的第二个

无序列表: 
* 第一个
- 第二个
  - 第二个的第一个
  - 第二个的第二个
- 第三个
```

有序列表: 
1. 第一个
2. 第二个
3. 第三个
  1. 第三点的第一个
  2. 第三点的第二个

无序列表: 
* 第一个
- 第二个
  - 第二个的第一个
  - 第二个的第二个
- 第三个

### 6. 文本加粗、倾斜和删除线

文本的特殊格式比较简单，加粗是文本两侧加**，倾斜是文本两侧加*，加粗和倾斜一起是文本两侧加***，删除线是文本两侧加~~

```shell
**加粗**
*倾斜*
***加粗和倾斜***
~~删除线~~
```

**加粗**
*倾斜*
***加粗和倾斜***
~~删除线~~

### 7. 引用文本

```shell
>引用文本
```

>引用文本

### 8. 分割线

分割线写法很简单，只需要使用三个或三个以上 *** 或者 --- 即可。

```shell
***
******
---
------
```

***
******
---
------

### 9. 图片

1. [alt](url title)方式
 
图片的引用的基本语法是：[alt](url title)，alt为图片下方文字，title为图片说明，即鼠标放上去后显示文案，url为图片路径。

```shell
![风景图](https://gimg2.baidu.com/image_search/src=http%3A%2F%2F1812.img.pp.sohu.com.cn%2Fimages%2Fblog%2F2009%2F11%2F18%2F18%2F8%2F125b6560a6ag214.jpg&refer=http%3A%2F%2F1812.img.pp.sohu.com.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1621561120&t=d99b987e1a68ed50f149aa611e2ab62a "风景图片")
```

![风景图](https://gimg2.baidu.com/image_search/src=http%3A%2F%2F1812.img.pp.sohu.com.cn%2Fimages%2Fblog%2F2009%2F11%2F18%2F18%2F8%2F125b6560a6ag214.jpg&refer=http%3A%2F%2F1812.img.pp.sohu.com.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1621561120&t=d99b987e1a68ed50f149aa611e2ab62a "风景图片")

2. html标签方式

```shell
<div align=center><img width=400 src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2F1812.img.pp.sohu.com.cn%2Fimages%2Fblog%2F2009%2F11%2F18%2F18%2F8%2F125b6560a6ag214.jpg&refer=http%3A%2F%2F1812.img.pp.sohu.com.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1621561120&t=d99b987e1a68ed50f149aa611e2ab62a" /></div>
```

<div align=center><img width=400 src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2F1812.img.pp.sohu.com.cn%2Fimages%2Fblog%2F2009%2F11%2F18%2F18%2F8%2F125b6560a6ag214.jpg&refer=http%3A%2F%2F1812.img.pp.sohu.com.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1621561120&t=d99b987e1a68ed50f149aa611e2ab62a" /></div>

### 10. 超链接

超链接的格式和图片结构基本差不多，[超链接名称](url title)

```shell
[程序员学习圣地: 掘金](https://juejin.cn/)
```

[程序员学习圣地: 掘金](https://juejin.cn/)

### 11. 表格

表格的写法看上去很有意思，第一行可以写标题，然后第二行通过特殊标识区分表头和表内容，同时默认表格文字左对齐，如果想文本居中，可以通过第二行标识进行控制。

```shell
默认表格：
姓名 | 年龄 | 班级 | 成绩
-|:-|:-|:-|
张三 | 20 | 一班 | 90
张三 | 20 | 一班 | 80
张三 | 20 | 一班 | 70
张三 | 20 | 一班 | 99

表格文本居中：(注意第二行变化)
姓名 | 年龄 | 班级 | 成绩
:-:|:-:|:-:|:-:|
张三 | 20 | 一班 | 90
张三 | 20 | 一班 | 80
张三 | 20 | 一班 | 70
张三 | 20 | 一班 | 99
```

默认表格：
姓名 | 年龄 | 班级 | 成绩
-|:-|:-|:-|
张三 | 20 | 一班 | 90
张三 | 20 | 一班 | 80
张三 | 20 | 一班 | 70
张三 | 20 | 一班 | 99

表格文本居中：(注意第二行变化)
姓名 | 年龄 | 班级 | 成绩
:-:|:-:|:-:|:-:|
张三 | 20 | 一班 | 90
张三 | 20 | 一班 | 80
张三 | 20 | 一班 | 70
张三 | 20 | 一班 | 99

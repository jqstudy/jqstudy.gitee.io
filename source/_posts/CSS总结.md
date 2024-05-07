---
title: CSS面试总结
date: 2023-12-18 21:44:00
tags:
categories: web前端
---

#### 1. 介绍一下标准的 CSS 的盒子模型？低版本 IE 的盒子模型有什么不同的？

1. 有两种盒子模型：IE盒模型（border-box）、W3C标准盒模型（content-box）
2. 盒模型：分为内容（content）、填充（padding）、边界（margin）、边框（border）四个部分

IE盒模型和W3C标准盒模型的区别：

1. W3C标准盒模型：属性width，height只包含内容content，不包含border和padding
2. IE盒模型：属性width，height包含content、border和padding，指的是content
+padding+border。

&nbsp;&nbsp;在ie8+浏览器中使用哪个盒模型可以由box-sizing（CSS新增的属性）控制，默认值为content-box，即标准盒模型；如果将box-sizing设为border-box则用的是IE盒模型。如果在ie6，7，8中DOCTYPE缺失会将盒子模型解释为IE盒子模型。若在页面中声明了DOCTYPE类型，所有的浏览器都会把盒模型解释为W3C盒模型。

回答：

&nbsp;&nbsp;盒模型都是由四个部分组成的，分别是margin、border、padding和content。
&nbsp;&nbsp;标准盒模型和IE盒模型的区别在于设置width和height时，所对应的范围不同。标准盒模型的width和height属性的范围只包含了content，而IE盒模型的width和height属性的范围包含了border、padding和content。
&nbsp;&nbsp;一般来说，我们可以通过修改元素的box-sizing属性来改变元素的盒模型。

#### 2. CSS 选择器有哪些？

1. id选择器(#myid)
2. 类选择器(.myclassname)
3. 标签选择器(div,h1,p)
4. 后代选择器(h1,p)
5. 子选择器(ul>li)
6. 兄弟选择器(所有)(li~a)
7. 相邻兄弟选择器(li+a)
8. 属性选择器(a[rel="external"])
9. 伪类选择器(a:hover,li:nth-child)
10. 伪元素选择器(::before、::after)
11. 通配符选择器(*)

#### 3. ::before 和:after 中双冒号和单冒号有什么区别？解释一下这 2 个伪元素的作用

相关知识点：
- 单冒号 (:) 用于CSS3伪类，双冒号 (::) 用于CSS3伪元素。(伪元素由双冒号和伪元素名称组成)
- 双冒号是在当前规范中引入的，用于区分伪类和伪元素。不过浏览器需要同时支持旧的已经存在的伪元素写法，比如:first-line、:first-letter、:before、:after等，而新的在CSS3中引入的伪元素则不允许再支持旧的单冒号的写法。
- 想让插入的内容出现在其它内容前，使用::before，否者，使用::after；
- 在代码顺序上，::after生成的内容也比::before生成的内容靠后。如果按堆栈视角，::after生成的内容会在::before生成的内容之上。

回答：
&nbsp;&nbsp;在css3中使用单冒号来表示伪类，用双冒号来表示伪元素。但是为了兼容已有的伪元素的写法，在一些浏览器中也可以使用单冒号来表示伪元素。
&nbsp;&nbsp;伪类一般匹配的是元素的一些特殊状态，如hover、link等，而伪元素一般匹配的特殊的位置，比如after、before等。

#### 4. 伪类与伪元素的区别

&nbsp;&nbsp;css引入伪类和伪元素概念是为了格式化文档树以外的信息。也就是说，伪类和伪元素是用来修饰不在文档树中的部分，比如，一句话中的第一个字母，或者是列表中的第一个元素。

&nbsp;&nbsp;伪类用于当已有的元素处于某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的。比如说，当用户悬停在指定的元素时，我们可以通过:hover来描述这个元素的状态。

&nbsp;&nbsp;伪元素用于创建一些不在文档树中的元素，并为其添加样式。它们允许我们为元素的某些部分设置样式。比如说，我们可以通过::before来在一个元素前增加一些文本，并为这些文本添加样式。虽然用户可以看到这些文本，但是这些文本实际上不在文档树中。

&nbsp;&nbsp;有时你会发现伪元素使用了两个冒号（::）而不是一个冒号（:）。这是CSS3的一部分，并尝试区分伪类和伪元素。大多数浏览器都支持这两个值。按照规则应该使用（::）而不是（:），从而区分伪类和伪元素。但是，由于在旧版本的W3C规范并未对此进行特别区分，因此目前绝大多数的浏览器都支持使用这两种方式表示伪元素。

#### 5. CSS 中哪些属性可以继承？

相关资料：

- 每个CSS属性定义的概述都指出了这个属性是默认继承的，还是默认不继承的。这决定了当你没有为元素的属性指定值时该如何计算值。
- 当元素的一个继承属性没有指定值时，则取父元素的同属性的计算值。只有文档根元素取该属性的概述中给定的初始值（这里的意思应该是在该属性本身的定义中的默认值）。
- 当元素的一个非继承属性（在Mozilla code里有时称之为reset property）没有指定值时，则取属性的初始值initial value（该值在该属性的概述里被指定）。

有继承性的属性：
- 字体系列属性font、font-family、font-weight、font-size、font-style、font-variant、font-stretch、font-size-adjust
- 文本系列属性text-indent、text-align、text-shadow、line-height、word-spacing、letter-spacing、
text-transform、direction、color
- 表格布局属性caption-side border-collapse empty-cells
- 列表属性list-style-type、list-style-image、list-style-position、list-style
- 光标属性cursor
- 元素可见性visibility
- 还有一些不常用的；speak，page，设置嵌套引用的引号类型quotes等属性

注意：当一个属性不是继承属性时，可以使用inherit关键字指定一个属性应从父元素继承它的值，inherit关键字用于显式地指定继承性，可用于任何继承性/非继承性属性。

回答：
&nbsp;&nbsp;每一个属性在定义中都给出了这个属性是否具有继承性，一个具有继承性的属性会在没有指定值的时候，会使用父元素的同属性的值来作为自己的值。

&nbsp;&nbsp;一般具有继承性的属性有，字体相关的属性，font-size和font-weight等。文本相关的属性，color和text-align等。表格的一些布局属性、列表属性如list-style等。还有光标属性cursor、元素可见性visibility。

&nbsp;&nbsp;当一个属性不是继承属性的时候，我们也可以通过将它的值设置为inherit来使它从父元素那获取同名的属性值来继承。

#### 6. CSS 优先级算法如何计算？

相关知识点：

CSS的优先级是根据样式声明的特殊性值来判断的。
选择器的特殊性值分为四个等级，如下：
1. 内联样式选择器x,0,0,0
2. ID选择器0,x,0,0
3. class选择器/属性选择器/伪类选择器	0,0,x,0
4. 元素和伪元素选择器0,0,0,x

计算方法：
1. 每个等级的初始值为0
2. 每个等级的叠加为选择器出现的次数相加
3. 不可进位，比如0,99,99,99
4. 依次表示为：0,0,0,0
5. 每个等级计数之间没关联
6. 等级判断从左向右，如果某一位数值相同，则判断下一位数值
7. 如果两个优先级相同，则最后出现的优先级高，!important也适用
8. 通配符选择器的特殊性值为：0,0,0,0
9. 继承样式优先级最低，通配符样式优先级高于继承样式
10. !important（权重），它没有特殊性值，但它的优先级是最高的，为了方便记忆，可以认为它的特殊性值为1,0,0,0,0。

计算实例：
1. #demo a{color: orange;}/*特殊性值：0,1,0,1*/
2. div#demo a{color: red;}/*特殊性值：0,1,0,2*/

注意：
1. 样式应用时，css会先查看规则的权重（!important），加了权重的优先级最高，当权重相同的时候，会比较规则的特殊性。
2. 特殊性值越大的声明优先级越高。
3. 相同特殊性值的声明，根据样式引入的顺序，后声明的规则优先级高（距离元素出现最近的）
4. 部分浏览器由于字节溢出问题出现的进位表现不做考虑

回答：
&nbsp;&nbsp;判断优先级时，首先我们会判断一条属性声明是否有权重，也就是是否在声明后面加上了!important。一条声明如果加上了权重，那么它的优先级就是最高的，前提是它之后不再出现相同权重的声明。如果权重相同，我们则需要去比较匹配规则的特殊性。

&nbsp;&nbsp;一条匹配规则一般由多个选择器组成，一条规则的特殊性由组成它的选择器的特殊性累加而成。选择器的特殊性可以分为四个等级，第一个等级是行内样式，为1000，第二个等级是id选择器，为0100，第三个等级是类选择器、伪类选择器和属性选择器，为0010，第四个等级是元素选择器和伪元素选择器，为0001。规则中每出现一个选择器，就将它的特殊性进行叠加，这个叠加只限于对应的等级的叠加，不会产生进位。选择器特殊性值的比较是从左向右排序的，也就是说以1开头的特殊性值比所有以0开头的特殊性值要大。比如说特殊性值为1000的的规则优先级就要比特殊性值为0999的规则高。如果两个规则的特殊性值相等的时候，那么就会根据它们引入的顺序，后出现的规则的优先级最高。

#### 7. 关于伪类 LVHA 的解释?

&nbsp;&nbsp;a标签有四种状态：链接访问前、链接访问后、鼠标滑过、激活，分别对应四种伪类:link、:visited、:hover、:active；

当链接未访问过时：
1. 当鼠标滑过a链接时，满足:link和:hover两种状态，要改变a标签的颜色，就必须将:hover伪类在:link伪类后面声明；
2. 当鼠标点击激活a链接时，同时满足:link、:hover、:active三种状态，要显示a标签激活时的样式（:active），必须将:active声明放到:link和:hover之后。因此得出LVHA这个顺序。
&nbsp;&nbsp;当链接访问过时，情况基本同上，只不过需要将:link换成:visited。
&nbsp;&nbsp;这个顺序能不能变？可以，但也只有:link和:visited可以交换位置，因为一个链接要么访问过要么没访问过，不可能同时满足，也就不存在覆盖的问题。

#### 8. CSS3 新增伪类有那些？

1. elem:nth-child(n)选中父元素下的第n个子元素，并且这个子元素的标签名为elem，n可以接受具体的数值，也可以接受函数。
2. elem:nth-last-child(n)作用同上，不过是从后开始查找。
3. elem:last-child选中最后一个子元素。
4. elem:only-child如果elem是父元素下唯一的子元素，则选中之。
5. elem:nth-of-type(n)选中父元素下第n个elem类型元素，n可以接受具体的数值，也可以接受函数。
6. elem:first-of-type选中父元素下第一个elem类型元素。\
7. elem:last-of-type选中父元素下最后一个elem类型元素。
8. elem:only-of-type如果父元素下的子元素只有一个elem类型元素，则选中该元素。
9. elem:empty选中不包含子元素和内容的elem类型元素。
10. elem:target选择当前活动的elem元素。
11. :not(elem)选择非elem元素的每个元素。
12. :enabled 控制表单控件的禁用状态。
13. :disabled	控制表单控件的禁用状态。
14. :checked单选框或复选框被选中。

#### 9. 如何居中 div？

- 水平居中：给 div 设置一个宽度，然后添加 margin:0 auto 属性
```
div {
  width: 200px;
  margin: 0 auto;
}
```
- 水平居中，利用 text-align:center 实现
```
.container {
  text-align: center;
}
```
- 让绝对定位的 div 居中
```
div {
  position: absolute;
  width: 300px;
  height: 300px;
  margin: auto;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}
```
- 水平垂直居中一
```
/*确定容器的宽高宽500高300的层设置层的外边距div{*/
position: absolute;/*绝对定位*/
  width: 500px;
  height: 300px;
  top: 50%;
  left: 50%;
  margin: -150px 0 0 -250px;/*外边距为自身宽高的一半*/
  background-color: pink;/*方便看效果*/
}
```
- 水平垂直居中二
```
/*未知容器的宽高，利用`transform`属性*/
div {
  position: absolute; /*相对定位或绝对定位均可*/
  width: 500px;
  height: 300px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: pink; /*方便看效果*/
}
```
- 水平垂直居中三
```
/*利用flex布局实际使用时应考虑兼容性*/
.container {
  display: flex;
  align-items: center; /*垂直居中*/
  justify-content: center; /*水平居中*/
}
.containerdiv {
  width: 100px;
  height: 100px;
  background-color: pink; /*方便看效果*/
}
```
- 水平垂直居中四
```
/*利用text-align:center和vertical-align:middle属性*/
.container {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
  text-align: center;
  font-size: 0;
  white-space: nowrap;
  overflow: auto;
}

.container::after {
  content: '';
  display: inline-block;
  height: 100%;
  vertical-align: middle;
}

.box {
  display: inline-block;
  width: 500px;
  height: 400px;
  background-color: pink;
  white-space: normal;
  vertical-align: middle;
}
```

回答：
- 对于宽高固定的元素
  1. 我们可以利用margin:0 auto来实现元素的水平居中。
  2. 利用绝对定位，设置四个方向的值都为0，并将margin设置为auto，由于宽高固定，因此对应方向实现平分，可以实现水平和垂直方向上的居中。
  3. 利用绝对定位，先将元素的左上角通过top:50%和left:50%定位到页面的中心，然后再通过margin负值来调整元素
  的中心点到页面的中心。
  4. 利用绝对定位，先将元素的左上角通过top:50%和left:50%定位到页面的中心，然后再通过translate来调整元素
  的中心点到页面的中心。
  5. 使用flex布局，通过align-items:center和justify-content:center设置容器的垂直和水平方向上为居中对
  齐，然后它的子元素也可以实现垂直和水平的居中。
&nbsp;&nbsp;对于宽高不定的元素，上面的后面两种方法，可以实现元素的垂直和水平的居中。

#### 10. display 有哪些值？说明他们的作用。

- block	块类型。默认宽度为父元素宽度，可设置宽高，换行显示。
- none	元素不显示，并从文档流中移除。
- inline	行内元素类型。默认宽度为内容宽度，不可设置宽高，同行显示。
- inline-block 默认宽度为内容宽度，可以设置宽高，同行显示。
- list-item	像块类型元素一样显示，并添加样式列表标记。
- table	此元素会作为块级表格来显示。
- inherit	规定应该从父元素继承display属性的值。

#### 11. position 的值 relative 和 absolute 定位原点是？

相关知识点：

- absolute 生成绝对定位的元素，相对于值不为static的第一个父元素的padding box进行定位，也可以理解为离自己这一级元素最近的一级position设置为absolute或者relative的父元素的padding box的左上角为原点的。
- fixed（老IE不支持）生成固定定位的元素，相对于浏览器窗口进行定位。
- relative 生成相对定位的元素，相对于其元素本身所在文档流中的位置进行定位。
- static 默认值。没有定位，元素出现在正常的流中（忽略top,bottom,left,right,z-index声明）。
- inherit 规定从父元素继承position属性的值。

回答：

&nbsp;&nbsp;relative 定位的元素，是相对于元素本身所在文档流中的位置进行定位的。
&nbsp;&nbsp;absolute 定位的元素，是相对于它的第一个position值不为static的祖先元素的padding box来进行定位的。这句话我们可以这样来理解，我们首先需要找到绝对定位元素的一个position的值不为static的祖先元素，然后相对于这个祖先元素的padding box来定位，也就是说在计算定位距离的时候，padding的值也要算进去。

#### 12. CSS3 有哪些新特性？（根据项目回答）

- 新增各种CSS选择器	(:not(.input)：所有class不是“input”的节点)
- 圆角		 (border-radius:8px)
- 多列布局	 (multi-column layout)
- 阴影和反射 (Shadow\Reflect)
- 文字特效	 (text-shadow)
- 文本修饰	 (Text-decoration)
- 线性渐变   (linear-gradient)
- 旋转			 (transform：rotate) 缩放，平移，倾斜，动画，多背景
例如：transform:\scale(0.85,0.90)\translate(0px,-30px)\skew(-9deg,0deg)\Animation:

#### 13. 请解释一下 CSS3 的 Flex box（弹性盒布局模型），以及适用场景？

相关知识点：
&nbsp;&nbsp;Flex是FlexibleBox的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
&nbsp;&nbsp;任何一个容器都可以指定为Flex布局。行内元素也可以使用Flex布局。注意，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。
&nbsp;&nbsp;采用Flex布局的元素，称为Flex容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为Flex元素（flex item），简称"元素"。
&nbsp;&nbsp;容器默认存在两根轴：水平的主轴（main axis）和垂直的辅轴（cross axis），元素默认沿主轴排列。

以下6个属性设置在容器上:

1. flex-direction属性决定主轴的方向（即元素的排列方向）。
2. flex-wrap属性定义，如果一条轴线排不下，如何换行。
3. flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
4. justify-content属性定义了元素在主轴上的对齐方式。 可选值：flex-start, flex-end, center, space-around,space-between, stretch
5. align-items属性定义元素在辅轴上如何对齐。 可选值：flex-start, flex-end, center， stretch
6. align-content属性定义了多根轴线的对齐方式。如果元素只有一根轴线，该属性不起作用。

以下6个属性设置在元素上:
1. order属性定义元素的排列顺序。数值越小，排列越靠前，默认为0
2. flex-grow属性定义元素的增长系数，默认为0，即如果存在剩余空间，也不放大。
3. flex-shrink属性定义了项目的缩减系数，默认为1，即如果空间不足，该项目将缩小。
4. flex-basis属性定义了在分配多余空间之前，元素占据的主轴空间。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
5. flex属性是flex-grow，flex-shrink和flex-basis的简写，默认值为0 1 auto。
6. align-self属性允许单个元素有与其他元素不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父
元素的align-items属性，如果没有父元素，则等同于stretch。

回答：

&nbsp;&nbsp;flex布局是CSS3新增的一种布局方式，我们可以通过将一个元素的display属性值设置为flex从而使它成为一个flex容器，它的所有子元素都会成为它的弹性元素。

&nbsp;&nbsp;一个容器默认有两条轴，一个是水平的主轴，一个是与主轴垂直的辅轴。我们可以使用flex-direction来指定主轴的方向。我们可以使用justify-content来指定元素在主轴上的排列方式，使用align-items来指定元素在辅轴上的排列方式。还可以使用flex-wrap来规定当一行排列不下时的换行方式。

&nbsp;&nbsp;对于容器中的弹性元素，我们可以使用order属性来指定元素的排列顺序，还可以使用flex-grow来指定当排列空间有剩余的时候，元素的增长系数。还可以使用flex-shrink来指定当排列空间不足时，元素的缩减系数。

#### 14. 用纯 CSS 创建一个三角形的原理是什么？
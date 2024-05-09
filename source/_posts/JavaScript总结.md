---
title: JavaScript总结
date: 2024-05-09 10:43:41
tags: [JavaScript, ES6, 动态语言特性, 现代Web开发]
categories: web前端
---

#### 1. 介绍 js 的基本数据类型。

&nbsp;&nbsp;`js`一共有七种基本数据类型，分别是`Undefined、Null、Boolean、Number、String`，还有在 `ES6` 中新增的 `Symbol` 和 `ES10` 中新增的 `BigInt` 类型。
&nbsp;&nbsp;`Symbol` 代表创建后独一无二且不可变的数据类型，它的出现我认为主要是为了解决可能出现的全局变量冲突的问题。
&nbsp;&nbsp;`BigInt` 是一种数字类型的数据，它可以表示任意精度格式的整数，使用 `BigInt` 可以安全地存储和操作大整数，即使这个数已经超出了 `Number` 能够表示的安全整数范围。

#### 2. JavaScript 有几种类型的值？你能画一下他们的内存图吗？

**涉及知识点：**
- 栈：原始数据类型（Undefined、Null、Boolean、Number、String）
- 堆：引用数据类型（对象、数组和函数）

两种类型的区别是：存储位置不同。
原始数据类型直接存储在栈（stack）中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储。

引用数据类型存储在堆（heap）中的对象，占据空间大、大小不固定。如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体。

**回答：**

  - js 可以分为两种类型的值，一种是基本数据类型，一种是引用数据类型。
  - 基本数据类型....（参考1）
  - 引用数据类型指的是 Object 类型，所有其他的如 Array、Date 等数据类型都可以理解为 Object 类型的子类。
  - 两种类型间的主要区别是它们的存储位置不同，基本数据类型的值直接保存在栈中，而复杂数据类型的值保存在堆中，通过使用在栈中保存对应的指针来获取堆中的值。

详细资料可以参考：
  [《JavaScript 有几种类型的值？》](https://blog.csdn.net/lxcao/article/details/52749421)
  [《JavaScript 有几种类型的值？能否画一下它们的内存图；》](https://blog.csdn.net/jiangjuanjaun/article/details/80327342)

#### 3. 什么是堆？什么是栈？它们之间有什么区别和联系？

- 堆和栈的概念存在于数据结构中和操作系统内存中。
- 在数据结构中，栈中数据的存取方式为先进后出。而堆是一个优先队列，是按优先级来进行排序的，优先级可以按照大小来规定。完全二叉树是堆的一种实现方式。
- 在操作系统中，内存被分为栈区和堆区。
- 栈区内存由编译器自动分配释放，存放函数的参数值，局部变量的值等。其操作方式类似于数据结构中的栈。
- 堆区内存一般由程序员分配释放，若程序员不释放，程序结束时可能由垃圾回收机制回收。

详细资料可以参考：[《什么是堆？什么是栈？他们之间有什么区别和联系？》](https://www.zhihu.com/question/19729973)

#### <font color="red">4. 内部属性 [[Class]] 是什么？</font>

```javascript
/*所有 typeof 返回值为 "object" 的对象（如数组）都包含一个内部属性 [[Class]]（我们可以把它看作一个内部的分类，而非
传统的面向对象意义上的类）。这个属性无法直接访问，一般通过 Object.prototype.toString(..) 来查看。例如：*/

Object.prototype.toString.call( [1,2,3] );
// "[object Array]"

Object.prototype.toString.call( /regex-literal/i );
// "[object RegExp]"

// 我们自己创建的类就不会有这份特殊待遇，因为 toString() 找不到 toStringTag 属性时只好返回默认的 Object 标签
// 默认情况类的[[Class]]返回[object Object]
class Class1 {}
Object.prototype.toString.call(new Class1()); // "[object Object]"
// 需要定制[[Class]]
class Class2 {
  get [Symbol.toStringTag]() {
    return "Class2";
  }
}
Object.prototype.toString.call(new Class2()); // "[object Class2]"
```

#### 5. 介绍 js 有哪些内置对象？

**涉及知识点：**

&nbsp;&nbsp;全局的对象（ global objects ）或称标准内置对象，不要和 "全局对象（global object）" 混淆。这里说的全局的对象是说在全局作用域里的对象。全局作用域中的其他对象可以由用户的脚本创建或由宿主程序提供。

标准内置对象的分类:
  1. 值属性，这些全局属性返回一个简单值，这些值没有自己的属性和方法。例: `Infinity、NaN、undefined、null` 字面量
  2. 函数属性，全局函数可以直接调用，不需要在调用时指定所属对象，执行结束后会将结果直接返回给调用者。例: `eval()、parseFloat()、parseInt()` 等
  3. 基本对象，基本对象是定义或使用其他对象的基础。基本对象包括一般对象、函数对象和错误对象。例: `Object、Function、Boolean、Symbol、Error` 等
  4. 数字和日期对象，用来表示数字、日期和执行数学计算的对象。例: `Number、Math、Date`
  5. 字符串，用来表示和操作字符串的对象。例: `String、RegExp`
  6. 可索引的集合对象，这些对象表示按照索引值来排序的数据集合，包括数组和类型数组，以及类数组结构的对象。例: `Array`
  7. 使用键的集合对象，这些集合对象在存储数据时会使用到键，支持按照插入顺序来迭代元素。例: `Map、Set、WeakMap、WeakSet`
  8. 矢量集合，SIMD 矢量集合中的数据会被组织为一个数据序列。例: `SIMD` 等
  9. 结构化数据，这些对象用来表示和操作结构化的缓冲区数据，或使用 JSON 编码的数据。例: `JSON` 等
  10. 控制抽象对象。例: `Promise、Generator` 等
  11. 反射。例: `Reflect、Proxy`
  12. 国际化，为了支持多语言处理而加入 ECMAScript 的对象。例: `Intl、Intl.Collator` 等
  13. WebAssembly。
  14. 其他。例: `arguments`

**回答：**

&nbsp;&nbsp;`js` 中的内置对象主要指的是在程序执行前存在全局作用域里的由 `js` 定义的一些全局值属性、函数和用来实例化其他对象的构造函
数对象。一般我们经常用到的如全局变量值 `NaN、undefined`，全局函数如 `parseInt()、parseFloat() `用来实例化对象的构
造函数如 `Date、Object` 等，还有提供数学计算的单体内置对象如 `Math` 对象。

详细资料可以参考：
  [《标准内置对象的分类》](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects)
  [《JS 所有内置对象属性和方法汇总》](https://segmentfault.com/a/1190000011467723#articleHeader24)

#### 6. undefined 与 undeclared 的区别？

- 已在作用域中声明但还没有赋值的变量，是 `undefined` 的。相反，还没有在作用域中声明过的变量，是 `undeclared` 的。
- 对于 `undeclared` 变量的引用，浏览器会报引用错误，如 `ReferenceError: b is not defined` 。
- 并且 `typeof` 对 `undefined` 和 `undeclared` 变量返回的都是`undefined`。其实`"undefined"` 和`"is not defined"`是两码事。

#### 7. null 和 undefined 的区别？

```
  首先 Undefined 和 Null 都是基本数据类型，这两个基本数据类型分别都只有一个值，就是 undefined 和 null。

  undefined 代表的含义是未定义，null 代表的含义是空对象。一般变量声明了但还没有赋值的时候会返回 undefined，null
  主要用于赋值给一些可能会返回对象的变量，作为初始化。

  undefined 在 js 中不是一个保留字，这意味着我们可以使用 undefined 来作为一个变量名，这样的做法是非常危险的，它
  会影响我们对 undefined 值的判断。但是我们可以通过一些方法获得安全的 undefined 值，比如说 void 0。

  当我们对两种类型使用 typeof 进行判断的时候，Null 类型化会返回 “object”，这是一个历史遗留的问题。当我们使用双等
  号对两种类型的值进行比较时会返回 true，使用三个等号时会返回 false。
  null == undefined    // true
  null === undefined   // false   数据类型不同
```

详细资料可以参考：[《JavaScript 深入理解之 undefined 与 null》](http://cavszhouyou.top/)

#### 8. 如何获取安全的 undefined 值？

&nbsp;&nbsp;因为 `undefined` 是一个标识符，所以可以被当作变量来使用和赋值，但是这样会影响 `undefined` 的正常判断。

&nbsp;&nbsp;表达式 `void ___` 没有返回值，因此返回结果是 `undefined。void` 并不改变表达式的结果，只是让表达式不返回值。

  - 按惯例我们用 `void 0` 来获得 `undefined`。
  - 除了防止被重写外，还可以减少字节。`void 0` 代替 `undefined`省3个字节。（老司机常用）

#### 9. 说几条写 JavaScript 的基本规范？

在平常项目开发中，我们遵守一些这样的基本规范，比如说：

1. 一个函数作用域中所有的变量声明应该尽量提到函数首部，用一个 `var` 声明，不允许出现两个连续的 `var` 声明，声明时如果变量没有值，应该给该变量赋值对应类型的初始值，便于他人阅读代码时，能够一目了然的知道变量对应的类型值。
2. 代码中出现地址、时间等字符串时需要使用常量代替。
3. 在进行比较的时候吧，尽量使用`'===', '!=='`代替`'==', '!='`。
4. 不要在内置对象的原型上添加方法，如 `Array, Date`。
5. `switch` 语句必须带有 `default` 分支。
6. `for` 循环必须使用大括号。
7. `if` 语句必须使用大括号。

#### 10. JavaScript 原型，原型链？ 有什么特点？

**什么是原型对象:**
1. 每个函数都有一个`prototype`属性，该属性指向的是原型对象(显示原型对象)
2. 每个实例对象身上都有一个`__proto__`属性，该属性指向的也是原型对象(隐式原型对象)
3. 构造函数的显示原型 `===` 当前构造函数实例对象的隐式原型对象
4. 原型对象的本质： 普通的`Object`实例

**什么是原型链：**
1. 查找对象的属性的时候现在自身找，如果自身没有沿着`__proto__`找原型对象
2. 如果原型对象上还没有，继续沿着`__proto__`,直到找到`Object`的原型对象
3. 如果还没有找到返回`undefined`
4. 原型链：沿着`__proto__`查找属性(方法)的这条链就是原型链

详细资料可以参考：[《JavaScript 深入理解之原型与原型链》](http://cavszhouyou.top/JavaScript%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3%E4%B9%8B%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%8E%9F%E5%9E%8B%E9%93%BE.html)

#### 11. js 获取原型的方法？

```javascript
  function R(){}
  var one = new R();
  console.log(Object.getPrototypeOf(one));	//官方推荐，规范写法
  console.log(one.proto);						//不报错，不推荐
  console.log(one.constructor.proto)	//同上
```

#### 12. 在 js 中不同进制数字的表示方式

- 以 0X、0x 开头的表示为十六进制。

- 以 0、0O、0o 开头的表示为八进制。

- 以 0B、0b 开头的表示为二进制格式。

#### 13. js 中整数的安全范围是多少？

&nbsp;&nbsp;安全整数指的是，在这个范围内的整数转化为二进制存储的时候不会出现精度丢失，能够被“安全”呈现的最大整数是 `2^53 - 1`，即`9007199254740991`，在 `ES6` 中被定义为 `Number.MAX_SAFE_INTEGER`。最小整数是`-9007199254740991`，在 ES6 中被定义为 `Number.MIN_SAFE_INTEGER`。

&nbsp;&nbsp;如果某次计算的结果得到了一个超过 `JavaScript` 数值范围的值，那么这个值会被自动转换为特殊的 `Infinity` 值。如果某次计算返回了正或负的 `Infinity` 值，那么该值将无法参与下一次的计算。判断一个数是不是有穷的，可以使用 `isFinite` 函数来判断。


#### <font color="red">14. typeof NaN 的结果是什么？</font>

&nbsp;&nbsp;`NaN` 意指“不是一个数字”（not a number），`NaN` 是一个“警戒值”（sentinel value，有特殊用途的常规值），用于指出
数字类型中的错误情况，即“执行数学运算没有成功，这是失败后返回的结果”。

`typeof NaN; // "number"`
`NaN` 是一个特殊值，它和自身不相等，是唯一一个非自反（自反，reflexive，即 x === x 不成立）的值。而 `NaN != NaN`为 `true`。

## 15. isNaN 和 Number.isNaN 函数的区别？

&nbsp;&nbsp;函数 isNaN 接收参数后，会尝试将这个参数转换为数值，任何不能被转换为数值的的值都会返回 true，因此非数字值传入也会返回 true ，会影响 NaN 的判断。

&nbsp;&nbsp;函数 Number.isNaN 会首先判断传入参数是否为数字，如果是数字再继续判断是否为 NaN ，这种方法对于 NaN 的判断更为准确。

#### 16. Array 构造函数只有一个参数值时的表现？

&nbsp;&nbsp;`Array` 构造函数只带一个数字参数的时候，该参数会被作为数组的预设长度`length`，而非只充当数组中的一个元素。这样
创建出来的只是一个空数组，只不过它的 `length` 属性被设置成了指定的值。

&nbsp;&nbsp;构造函数 `Array(..)` 不要求必须带 `new` 关键字。不带时，它会被自动补上。

#### 17. 其他值到字符串的转换规则？

**规范的 9.8 节中定义了抽象操作 ToString ，它负责处理非字符串到字符串的强制类型转换:**
  1. `Null` 和 `Undefined` 类型 ，`null` 转换为 `"null"`，`undefined` 转换为 `"undefined"`。
  2. `Boolean` 类型，`true` 转换为 `"true"`，`false` 转换为 `"false"`。
  3. `Number` 类型的值直接转换，不过那些极小和极大的数字会使用指数形式。
  4. `Symbol` 类型的值直接转换，但是只允许显式强制类型转换，使用隐式强制类型转换会产生错误。
  5. 对普通对象来说，除非自行定义 `toString()` 方法，否则会调用 `toString(): Object.prototype.toString()`来返回内部属性 `[[Class]]` 的值，如`"[object Object]"`。如果对象有自己的 `toString()` 方法，字符串化时就会调用该方法并使用其返回值。

#### 18. 其他值到数字值的转换规则？

&nbsp;&nbsp;有时我们需要将非数字值当作数字来使用，比如数学运算。为此 ES5 规范在 9.3 节定义了抽象操作 ToNumber。
  1. `Undefined` 类型的值转换为 `NaN`。
  2. `Null` 类型的值转换为 `0`。
  3. `Boolean` 类型的值，`true` 转换为 `1`，`false` 转换为 `0`。
  4. `String` 类型的值转换如同使用 `Number()` 函数进行转换，如果包含非数字值则转换为 `NaN`，空字符串为 `0`。
  5. `Symbol` 类型的值不能转换为数字，会报错。
  6. 对象（包括数组）会首先被转换为相应的基本类型值，如果返回的是非数字的基本类型值，则再遵循以上规则将其强制转换为数字。

&nbsp;&nbsp;为了将值转换为相应的基本类型值，抽象操作 `ToPrimitive` 会首先（通过内部操作 DefaultValue）检查该值是否有`valueOf()` 方法。如果有并且返回基本类型值，就使用该值进行强制类型转换。如果没有就使用 `toString()` 的返回值（如果存在）来进行强制类型转换。

&nbsp;&nbsp;如果 `valueOf()` 和 `toString()` 均不返回基本类型值，会产生 `TypeError` 错误。

#### 19. 其他值到布尔类型的值的转换规则？

  ES5 规范 9.2 节中定义了抽象操作 ToBoolean，列举了布尔强制类型转换所有可能出现的结果。
  **以下这些是假值：**
  - undefined
  - null
  - false
  - +0、-0 和 NaN
  - ""(空串)
  假值的布尔强制类型转换结果为 false。从逻辑上说，假值列表以外的都应该是真值。

#### <font color="red">20. {} 和 [] 的 valueOf 和 toString 的结果是什么？</font>

`{} 的 valueOf 结果为 {} ，toString 的结果为 "[object Object]"`

`[] 的 valueOf 结果为 [] ，toString 的结果为 "" （空串）`

#### 21. 什么是假值对象？

&nbsp;&nbsp;浏览器在某些特定情况下，在常规 `JavaScript` 语法基础上自己创建了一些外来值，这些就是“假值对象”。假值对象看起来和普通对象并无二致（都有属性，等等），但将它们强制类型转换为布尔值时结果为 `false` 最常见的例子是 `document.all`，它是一个类数组对象，包含了页面上的所有元素，由 `DOM(而不是 JavaScript 引擎)`提供给 `JavaScript` 程序使用。

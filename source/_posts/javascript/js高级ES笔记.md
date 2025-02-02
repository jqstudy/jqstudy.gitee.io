---
title: js高级ES笔记
date: 2024-05-15 13:55:25
tags: JavaScript高级
categories: JavaScript
---

### 1. **理解ECMAScript**
1. 全称: ECMAScript
2. js语言的规范
3. 我们用的js是它的实现
4. js的组成
  * ECMAScript(js基础)
  * 扩展-->浏览器端
    * BOM
    * DOM
  * 扩展-->服务器端
    * Node.js
      
### 2. ES5
1. **严格模式**
  * 运行模式: 正常(混杂)模式与严格模式
  * 应用上严格式: 'strict mode';
  * 作用: 
    * 使得Javascript在更严格的条件下运行
    * 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为
    * 消除代码运行的一些不安全之处，保证代码运行的安全
    * 需要记住的几个变化
      * 声明定义变量必须用var
      * 禁止自定义的函数中的this关键字指向全局对象
      * 创建eval作用域, 更安全
      
2. **JSON对象**
  * 作用: 用于在json对象/数组与js对象/数组相互转换
  * JSON.stringify(obj/arr)
      js对象(数组)转换为json对象(数组)
  * JSON.parse(json)
      json对象(数组)转换为js对象(数组)
      
3. Object扩展
  * Object.create(prototype[, descriptors]) : 创建一个新的对象
    * 以指定对象为原型创建新的对象
    * 指定新的属性, 并对属性进行描述
      * value : 指定值
      * writable : 标识当前属性值是否是可修改的, 默认为true
      * **get方法** : 用来得到当前属性值的回调函数
      * **set方法** : 用来监视当前属性值变化的回调函数
  * Object.defineProperties(object, descriptors) : 为指定对象定义扩展多个属性

4. Array扩展
  * Array.prototype.indexOf(value) : 得到值在数组中的第一个下标
  * Array.prototype.lastIndexOf(value) : 得到值在数组中的最后一个下标
  * **Array.prototype.forEach(function(item, index){}) : 遍历数组**
  * **Array.prototype.map(function(item, index){}) : 遍历数组返回一个新的数组**
  * **Array.prototype.filter(function(item, index){}) : 遍历过滤出一个子数组**

5. **Function扩展**
  * Function.prototype.bind(obj)
      * 将函数内的this绑定为obj, 并将函数返回
  * 面试题: 区别bind()与call()和apply()?
      * fn.bind(obj) : 指定函数中的this, 并返回函数
      * fn.call(obj) : 指定函数中的this,并调用函数
      
6. Date扩展
  * Date.now() : 得到当前时间值

### 3. ES6
1. **2个新的关键字**
  * let/const
  * 块作用域
  * 没有变量提升（不准确）
  * 不能重复定义
  * 值不可变

  - **let**
     - 作用：同var一样用来声明变量
     - 变量提升：
        - 全局变量提升
            - 会创建一个变量对象（script）用来收集全局作用域下let定义的变量，但是没有赋值
        - 局部变量提升
            - 会将var let定义的变量全部放到当前函数的变量对象中
        - 同var的变量提升的区别
            - let提升的变量在未赋值之前不允许被使用

  - **const**
     - 作用：定有常量
     - 特点：定义的常量不可以被修改

2. **变量的解构赋值**
     * 将包含多个数据的对象(数组)一次赋值给多个变量
     * 数据源: 对象/数组
     * 目标: {a, b}/[a, b]
     
3. **各种数据类型的扩展**
  * 字符串
    * **模板字符串** 
      * 作用: 简化字符串的拼接
      * 模板字符串必须用``
      * 变化的部分使用${xxx}定义
    * contains(str) : 判断是否包含指定的字符串
    * startsWith(str) : 判断是否以指定字符串开头
    * endsWith(str) : 判断是否以指定字符串结尾
    * repeat(count) : 重复指定次数
    
  * 对象
    * **简化的对象写法**
      ```
      let name = 'Tom';
      let age = 12;
      let person = {
          name,
          age,
          setName (name) {
              this.name = name;
          }
      };
      ```
    * Object.assign(target, source1, source2..) : 将源对象的属性复制到目标对象上
    * Object.is(v1, v2) : 判断2个数据是否完全相等
    * __proto__属性 : 隐式原型属性
    
  * 数组
    * Array.from(v) : 将伪数组对象或可遍历对象转换为真数组
    * Array.of(v1, v2, v3) : 将一系列值转换成数组
    * find(function(value, index, arr){return true}) : 找出第一个满足条件返回true的元素
    * findIndex(function(value, index, arr){return true}) : 找出第一个满足条件返回true的元素下标
  * 函数
    * **箭头函数**
      * 用来定义匿名函数
      * 基本语法:
        * 没有参数: () => console.log('xxxx')
        * 一个参数: i => i+2
        * 大于一个参数: (i,j) => i+j
        * 函数体不用大括号: 默认返回结果
        * 函数体如果有多个语句, 需要用{}包围
      * 使用场景: 多用来定义回调函数
      * 特点：
        * this：箭头函数没有自己的this，不是调用的时候决定的，而是定义的时候决定的
        * 理解：
              - 看定义的时候外部是否有函数，如果有当前箭头函数的this同外部函数的this指向是同一个对象
                  - 如果没有，箭头函数this指向的是window
        * 箭头函数不能用作构造函数
    * **形参的默认值**
      * 定义形参时指定其默认的值
    * **三点运算符**
      * **rest(可变)参数**
        1. 通过形参左侧的...来表达, 取代arguments的使用
        2. 它比arguments更加灵活
        3. 同样是来收集函数的实参列表
        4. 使用三点运算符收集的是一个真数组
        5. 可以根据需求收集指定的参数
      * **扩展运算符(拆包)**
        * 语法：...arr
        * 作用：可以分解出数组中的数据
        * 原理：三点运算符会调用iterator接口，如果底层有这个接口，那就可以去遍历数组
  * Symbol
    1. 理解：ES6提供的一种新的数据类型
    2. 基本数据类型：string, number, boolean, undefined, null, symbol, 
    3. typeof返回值：number, string, boolean, undefined, object, function, symbol 
    4. symbol特点：值是唯一的

4. iterator遍历器对象

```js
function iteratorUtil() { // iterator接口 ： 方法 || api
    console.log('我的方法被调用了', this); // this是遍历的目标数组或目标对象
    // console.log(target);// undefined
    // 缓存this
    let that = this;
    let index = 0; //  标识指针的起始位置
    let keys = Object.keys(that);// 获取对象中所有key的数组
    if(this instanceof Array){ // 遍历数组
      return { // 生成iterator遍历器对象
        next:  function (){ // 可以使用箭头函数解决this的指向问题
          return index < that.length ? {value: that[index++], done: false} : {value: that[index++], done: 					true}
        }
      }
    }else {// 遍历对象
      return { // 生成iterator遍历器对象
        next:  function (){ // 可以使用箭头函数解决this的指向问题
          return index < keys.length?{value: that[keys[index++]], done: false}:{value: 									that[keys[index++]], done: true}
        }
      }
    }
  }

  Array.prototype[Symbol.iterator] = iteratorUtil;
  Object.prototype[Symbol.iterator] = iteratorUtil;
```

5. set/Map容器结构
  * 容器: 能保存多个数据的对象, 同时必须具备操作内部数据的方法
  * 任意对象都可以作为容器使用, 但有的对象不太适合作为容器使用(如函数)
  * **Set的特点**: 保存多个value, value是不重复 ====>数组元素去重
  * **Map的特点**: 保存多个key--value, key是不重复, value是可以重复的
  * API
    * Set()/Set(arr) //arr是一维数组
    * add(value)
    * delete(value)
    * clear();
    * has(value)
    * size
    * 
    * Map()/Map(arr) //arr是二维数组
    * set(key, value)
    * get(key)
    * clear()
    * has(key)
    * size
    
5. **for--of循环**
  * 可以遍历任何容器
  * 数组
  * 伪/类数组
  * 字符串
  * 可迭代的对象

6. **Promise**
  * 解决`回调地狱`(回调函数的层层嵌套, 编码是不断向右扩展, 阅读性很差)
  * 能以同步编码的方式实现异步调用
  * 在es6之前原生的js中是没这种实现的, 一些第三方框架(jQuery)实现了promise
  * ES6中定义实现API: 
    ```
    // 1. 创建promise对象
    var promise = new Promise(function(resolve, reject){ 
      // 做异步的操作 
      if(成功) { // 调用成功的回调
        resolve(result); 
      } else { // 调用失败的回调
        reject(errorMsg); 
      } 
    }) 
    // 2. 调用promise对象的then()
    promise.then(function(
      result => console.log(result), 
      errorMsg => alert(errorMsg)
    ))
    ```
7. **class类**
  * 用 class 定义一类
  * 用 constructor() 定义构造方法(相当于构造函数)
  * 一般方法: xxx () {}
  * 用extends来定义子类
  * 用super()来继承父类的构造方法
  * 子类方法自定义: 将从父类中继承来的方法重新实现一遍
  * js中没有方法重载(方法名相同, 但参数不同)的语法

8. **模块化(后面讲)**

### 4. ES7
* 指数运算符: **
* Array.prototype.includes(value) : 判断数组中是否包含指定value
  
* **区别方法的2种称谓**
  * 静态(工具)方法
    * Fun.xxx = function(){}
  * 实例方法
    * 所有实例对象 : Fun.prototype.xxx = function(){} //xxx针对Fun的所有实例对象
    * 某个实例对象 : fun.xxx = function(){} //xxx只是针对fun对象
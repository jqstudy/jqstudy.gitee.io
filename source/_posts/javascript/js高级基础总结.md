---
title: js高级基础总结
date: 2024-05-15 13:51:57
tags: JavaScript高级
categories: JavaScript
---

# 1. 数据类型的分类和判断
## 1). 基本(值)类型
    Number ----- 任意数值 -------- typeof
    String ----- 任意字符串 ------ typeof
    Boolean ---- true/false ----- typeof
    undefined --- undefined ----- typeof/===
    null -------- null ---------- ===
## 2). 对象(引用)类型
	Object ----- typeof/instanceof
	Array ------ instanceof
	Function ---- typeof/instanceof

# 2. 数据,变量, 内存的理解
## 1). 什么是数据?
	在内存中可读的, 可传递的保存了特定信息的'东东'
	一切皆数据, 函数也是数据
	在内存中的所有操作的目标: 数据
## 2). 什么是变量?
	在程序运行过程中它的值是允许改变的量
	一个变量对应一块小内存, 它的值保存在此内存中  
## 3). 什么是内存?
	内存条通电后产生的存储空间(临时的)
	一块内存包含2个方面的数据
		内部存储的数据
		地址值数据
	内存空间的分类
		栈空间: 全局变量和局部变量
		堆空间: 对象 
## 4). 内存,数据, 变量三者之间的关系
	内存是容器, 用来存储不同数据
	变量是内存的标识, 通过变量我们可以操作(读/写)内存中的数据  

# 3. 对象的理解和使用
## 1). 什么是对象?
	多个数据(属性)的集合
	用来保存多个数据(属性)的容器
## 2). 属性组成:
	属性名 : 字符串(标识)
	属性值 : 任意类型
## 3). 属性的分类:
	一般 : 属性值不是function  描述对象的状态
	方法 : 属性值为function的属性  描述对象的行为
## 4). 特别的对象
	数组: 属性名是0,1,2,3之类的索引
	函数: 可以执行的
## 5). 如何操作内部属性(方法)
	.属性名
	['属性名']: 属性名有特殊字符/属性名是一个变量

# 4. 函数的理解和使用
## 1). 什么是函数?
    用来实现特定功能的, n条语句的封装体
    只有函数类型的数据是可以执行的, 其它的都不可以
## 2). 为什么要用函数?
    提高复用性
    便于阅读交流
## 3). 函数也是对象
    function instanceof Object===true
    函数有属性: prototype
    函数有方法: call()/apply()
    可以添加新的属性/方法
## 4). 函数的四种不同角色
    一般函数 : 直接调用
    构造函数 : 通过new调用
    方法: 通过对象调用
    对象 : 通过.调用内部的属性/方法
## 5). 函数中的this
      1. 理解this：
         - 关键字
         - 变量
      2. this的指向问题
         - 函数this不是函数定义的时候决定的
         - 函数this指向谁看如何调用当前的函数
      3. this指向分类
         - 函数自调用： window
         - 构造函数(new function): 当前构造函数的实例对象
         - 对象.方法(): 对象本身
         - fun.call/apply(指定的对象): 指定的对象
## 6). 匿名函数自调用:
    (function(){
      //实现代码
    })()
    专业术语为: IIFE (Immediately Invoked Function Expression) 立即调用函数表达式						  
## 7). 回调函数的理解
    什么函数才是回调函数?
        你定义的
        你没有调用
        但它最终执行了(在一定条件下或某个时刻)
    常用的回调函数
        dom事件回调函数
        定时器回调函数
        ajax请求回调函数(后面讲解)
        生命周期回调函数(后面讲解)

# git管理项目
## 1). 创建本地仓库
    创建.gitignore配置文件
    git init
    git add *
    git commit -m "xxx"

## 2). 创建github远程仓库
    New Repository
    指定名称
    创建
## 3). 将本地仓库推送到远程仓库
    git remote add origin https://github.com/zxfjd3g/170612_JSAdvance.git 关联远程仓库
    git push origin master

## 4). push本地的更新 
    git add *
    git commit -m "xxx"
    git push origin master

## 5). 克隆github上的项目:
    git clone https://github.com/zxfjd3g/170612_JSAdvance.git

## 6). pull远程的更新
    git pull origin master

## 7). 撤消本地修改
    git status  查看变化
    git checkout -- xxx文件  撤消指定文件的修改
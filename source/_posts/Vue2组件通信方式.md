---
title: Vue2组件通信方式
date: 2023-09-14 13:49:45
tags: Vue2
categories: Vue
---

### 1. 通过 props 和 $emit 实现父子组件的传参

父组件
```javascript
<template>
  <div>
    <h1>{{ title }}</h1>
    <child :message="message" @update-message="updateMessage"></child>
  </div>
</template>
<script>
import Child from "./Child.vue"
export default {
  name: "Parent",
  components: { Child },
  data() {
    return { title: "Parent Component", message: "Hello World" }
  },
  methods: {
    updateMessage(newMessage) {
      this.message = newMessage
    }
  }
}
</script>
```

子组件
```javascript
<template>
  <div>
    <h1>{{ message }}</h1>
    <button @click="updateMessage">更新</button>
  </div>
</template>
<script>
export default {
  name: "Child",
  props: {
    message: {
      type: String,
      default: ''
    }
  },
  methods: {
    updateMessage() {
      this.$emit('update-message', '更新了')
    }
  }
}
</script>
```

### 2. 通过 $parent 和 $children 实现父子组件通信

- 通过 $parent 访问到的是上一级父组件的实例，可以使用 $root 来访问根组件的实例
- 在组件中使用$children拿到的是所有的子组件的实例，它是一个数组，并且是无序的
- 在根组件 #app 上拿 $parent 得到的是 new Vue()的实例，在这实例上再拿 $parent 得到的是undefined，而在最底层的子组件拿 $children 是个空数组
$children 的值是数组，而 $parent是个对象

父组件
```javascript
<template>
  <div>
    <h1>{{ title }}</h1>
    <child></child>
  </div>
</template>
<script>
import Child from "./Child.vue"
export default {
  name: "Parent",
  components: { Child },
  data() {
    return { title: "Parent Component", message: "Hello World" }
  },
  mounted() {
    console.log(this.$children[0].message)
  }
}
</script>
```

子组件
```javascript
<template>
  <div>
    <h1>{{ title }}</h1>
    <span>{{ message }}</span>
  </div>
</template>
<script>
export default {
  name: "Child",
  data() {
    title: '测试',
    message: 'hello word'
  },
  mounted() {
    this.title = this.$parent.title
  }
}
</script>
```

### 3. 兄弟组件传值 eventBus 事件总线

```javascript
新建一个.js的文件作为中间件，作为事件中心管理组件之间的通信，通过 $emit 自定义事件，$on 监听自定义事件

import Vue from 'vue'
// 定义一个新的vue实例作为事件中心，利用它来监听本身的自定义事件
const tmpCom = new Vue()
export default tmpCom
```

A组件
```javascript
<template>
  <div class="">
    <h4>A组件</h4>
    <input type="button" value="我是A组件" @click="maxbrother">
  </div>
</template>

<script>
 //引入中间件
import tmpCom from '@/router/middleware'
export default {
  data () {
    return {
      brotherdata: '我是大兄弟'
    }
  },
  methods: {
    maxbrother () {
       // 触发事件中心的max-brother事件 
      tmpCom.$emit('max-brother', this.brotherdata)
      console.log(this.brotherdata)
    }
  },
  created () {}
}
</script>
```

B组件
```javascript
<template>
  <div class="">
    <h4>B组件</h4>
    <p>{{brother}}</p>
  </div>
</template>

<script>
//引入中间件
import tmpCom from '@/router/middleware'
export default {
  data () {
    return {
      brother: '我是B组件'
    }
  },
  mounted () {
      // 监听事件中心的max-brother事件
     // 这里的第二个参数必须使用箭头函数
    tmpCom.$on('max-brother', val => {
      this.brother = val
    })
  }
}
</script>
```

### 4. 注入依赖 provide/inject 使用

这种方式就是vue中依赖注入，该方法用于 父子组件之间 的通信。当然这里所说的父子不一定是真正的父子，也可以是祖孙组件，在层数很深的情况下，可以使用这种方式来进行传值。就不用一层一层的传递数据了。

provide和inject是vue提供的两个钩子，和data、methods是同级的。并且provide的书写形式和data一样。

- provide 钩子用来发送数据或方法。
- inject钩子用来接收数据或方法

```javascript
//父组件  
data () {
    return {
      pimsg: '我是父组件的值',
      num: 99999
    }
  },
  provide () {
    return {
      num: this.num
    }
  }

//子组件
 inject: ['num']
```

### 5. ref / $refs

这种方式也是实现父子组件之间的通信

ref：这个属性用在子组件上，它的用法就指向了子组件的实例，可以通过实例来访问组件的数据和方法

```javascript
//子组件
export default {
    data () {
    return {
      name: '我是张三'
    }
  },
  methods: {
    sayHello () {
      console.log('我是李四')
    }
  }
}
```

```javascript
//父组件
<template>
  <child ref="child"></child>
</template>

<script>
  import child from './child.vue'
  export default {
    components: { child },
    mounted () {
      console.log(this.$refs.child.name);  // '我是张三'
      this.$refs.child.sayHello();  // 我是李四
    }
  }
</script>
```
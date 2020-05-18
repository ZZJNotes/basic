# Vue

## Vue概述

### Vue是什么

渐进式框架，采用自底向上增量开发的设计，Vue的和辛苦只关注视图层，Vue完全有能力驱动采用单文件组件和Vue生态系统支持开发复杂单页应用

- 渐进式：从核心到完备的全家桶
- 增量：从少到多，从一页到多页，从简单到复杂
- 单文件组件：一个文件描述一个组件
- 单页应用：经过打包生成要给单页的html文件和一些js文件

### Vue的优缺点

###缺点

- Vue不缺入门教程，可是很缺高阶教程和文档
- Vue不支持IE8
- 生态环境差不如angular和react
- 社区不大

### 优点

- Vue基本语法(简单)
  - 简洁，轻量，快速，数据驱动，模块友好，组件化
- Vue各种插件(完善)
  - Vue官方提供了一系列的工具
    - 路由vue-router
    - 状态树管理器vuex
    - 网络请求axios(非官方出)

## Vue基本语法

### 引入和差值表达式

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>vue</title>
    <!--引入vue.js最好放在head部分引入（避免页面抖屏）-->
    <script src="./vue.js"></script>
</head>
<body>
<!--<div id="root" > hello world</div>-->
<div id="root">{{msg}}</div>

<script>
    new  Vue({
        el:"#root",
        data:{
            msg: "hello date"
        }
    })
</script>

</body>
</html>
~~~



### v指令

####v-bind

单向绑定，用来绑定数据和属性以及表达式，缩写为`:`

```html
<body>

<!--v-bind:  单向绑定,
就是对绑定的属性(根据属性等于的字段)取值(向vue对象内取值)-->

<div id="root">
    {{msg}}
    <input v-bind:value="msg">
    <img :src="url">
</div>

<script>
    new Vue({
        el:'#root',
        data: {
            msg: 123,
            url: './1234.png'
        }
    })
</script>


</body>

```



####v-model

实现双向数据绑定

```html
// 根据输入框的内容的改变，图片的内容会变
<body>

v-model:  vue的双向绑定,
单向: 去取
双向: 去取,  但是, 改变了---会影响vue对象的值

<div id="root">
    {{url}}
    <input v-model:value="url">
    <img v-bind:src="url">
</div>

<script>
    new Vue({
        el:'#root',
        data: {
            url: './1234.png'
        }
    })
</script>

</body>
```



####v-text和v-html
- `v-text`类似更新元素的 `innerText`
- `v-html`类似更新元素的`innerHtml`

```html
//v-html会显示HTML的效果，<b></b>加粗
<body>

<div id="root">
    <div v-text="msg" onclick="f()">
    </div>
    <div v-html="msg">
    </div>
</div>
<script>

    function f() {
        alert(123)
    }

    new Vue({
        el: '#root',
        data: {
            msg: '<b>123</b>'
        }
    })
</script>

</body>
```

####v-show
标签控制隐藏,  (display设置none)

```html
//点击button改变了bool的值，v-show指令根据bool的真假控制隐藏
<body>
<div id="root">
    <div v-show="bool">
        123
    </div>
    <button @click="change1">改变</button>
</div>
<script>

    new Vue({
        el: '#root',
        data: {
            bool: false,
            mid: ''
        },
        methods: {
            change1: function () {
                this.bool = !this.bool
            },
            change2: function () {

            }
        }
    })
</script>
</body>
```
####v-if
- 根据表达式的值的真假条件渲染元素
- V-else，V-else-if

```html
<body>
<div id="root">
    <div v-if="bool">
        123
    </div>
    <div v-else-if="bool2">
        bool2
    </div>
    <div v-else>
        456
    </div>


    <button @click="change1">改变</button>
</div>
<script>

    new Vue({
        el: '#root',
        data: {
            bool: false,
            bool2: true
        },
        methods: {
            change1: function () {
                this.bool = !this.bool
            }
        }
    })
</script>
</body>
```
#####v-if和v-show的区别

- `v-show=false`只是把这个标签隐藏，但是这个标签还存在dom树中
- `v-if=false`是把`v-if`所在标签整个标签取消在dom中

####v-for
基于源数据多次渲染元素或模板块(循环渲染元素)
```html
//类似于遍历
<body>

<div id="root">
    <div v-for="aaa of list" :key="aaa.id">
        // of 也可以写成 in， :key不能少
        {{aaa.name}}---{{aaa.id}}
    </div>
</div>

<script>

    new Vue({
        el: '#root',
        data:{
           list: [
               {
                   id: 1,
                  name: 'zs'
               },
               {
                   id:2,
                   name: 'ls'
               },
               {
                   id:3,
                   name: 'wu'
               }
           ]
        }
    })

</script>

</body>
```
####v-on
绑定事件监听器。可简写`@`

```html
<body>
<div id="root">
    {{msg}}
    <button v-on:click="f">改变</button>
    //可以写成 @click
</div>

<script>
    new Vue({
        el: '#root',
        data: {
            msg: 123
        },
        methods: {
            f: function () {
                alert(123)
            }
        }
    })
</script>
</body>
```
####v-pre
v-pre可以用来阻止预编译，有v-pre指令的标签内部的内容不会被编译，会原样输出。

```html
<body>
<div id="root">
    <div v-pre>
        {{msg}}
        // 显示的是{{msg}}
    </div>
    {{msg}}
    // 显示的是123
</div>

<script>
    new Vue({
        el:'#root',
        data: {
            msg:123
        }
    })
</script>

</body>
```
####v-cloak
- 延迟显示
- 这个指令保持在元素上直到关联实例结束编译。和 CSS 规则如 `[v-cloak] { display: none }` 一起用时，这个指令可以隐藏未编译的 标签直到实例准备完毕



```html
<body>
<div id="root">
    <div v-cloak>
        {{msg}}
    </div>
</div>

<script>


    setTimeout('f()', 3000)
    function f() {
        new Vue({
            el: '#root',
            data: {
                msg: '123'
            }
        })
    }

    // setInterval('f()', 3000)

</script>

</body>
```
####v-once
只渲染元素和组件一次。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。

```html
<body>

<div id="root">
    <div v-once>
        {{msg}}
    </div>
    <input v-model:value="msg">
</div>

<script>
    new Vue({
        el: '#root',
        data: {
            msg: 123
        }
    })

</script>

</body>
```
### 计算属性

computed

- 指的是一个属性通过其他属性计算而来

```html
<body>

<div id="root">

    input1:<input v-model="input1"><br>
    input2:<input v-model="input2"><br>
    <button @click="add">相加</button>
    <hr>
    sum: {{sum}}<br>
    sum2: {{sum2}}<br>
    sum3: {{sum3}}<br>
    allSum: {{allsum}}
</div>
<script>

    new Vue({
        el: '#root',
        data: {
            input1: 0,
            input2: 0,
            sum: 0,
            allsum: 0
        },
        methods:{
            add: function () {
                this.sum = parseInt(this.input1) + parseInt(this.input2)

                this.allsum =  parseInt(this.input1) + parseInt(this.input2) + this.sum + this.sum2
            }
        },
        computed: {
            sum2: function () {
                return parseInt(this.input1) + parseInt(this.input2)
            },
            sum3: function () {
                return parseInt(this.input1) + parseInt(this.input2) + this.sum2
            }
        }
    })
</script>
</body>
```

#### 注意



### 侦听器

watch:

- 监听一个属性改变触发一个事件

```html
<body>

<div id="root">
    <input v-model="input1">
    <input v-model="input2"><br>
    和: {{sum}}<br>
    计算了几次: {{addTimes}}
</div>
<script>

    new Vue({
        el: '#root',
        data: {
            input1: 0,
            input2: 0,
            addTimes: 0
        },
        computed: {
            sum: function () {
                return parseInt(this.input1) + parseInt(this.input2)
            }
        },
        watch: {
            // input1: function () {
            //     this.addTimes ++
            // },
            // input2: function () {
            //     this.addTimes ++
            // }
            sum: function () {
                this.addTimes ++
            }
        }
    })



</script>

</body>
```



### 模板

`template`

- 一个字符串模板作为 Vue 实例的标识使用。模板将会 替换 挂载的元素。挂载元素的内容都将被忽略(除非模板的内容有分发插槽)

```html
<body>

<div id="root">
</div>

<script>

    new Vue({
        el: '#root',
        template: '<b><b @click="f1">{{msg}}</b></b>',
        //上面的会替换dom树中id="root"的div节点
        data: {
            msg: 123
        },
        methods: {
            f1: function () {
                alert(123)
            }
        }
    })
</script>
</body>
```



### 全局组件

`Vue.component`

```html
<body>

<div id="root">
    <aaa></aaa>
    <b-b-b></b-b-b>
</div>

<script>
    // 创建一个全局组件( vue对象)
    Vue.component('aaa', {
        template: '<div><div @click="f">aaa</div></div>',
        methods: {
            f: function () {
                alert(123)
            }
        }
    })

    Vue.component('BBB', {
        template: '<div>bbb</div>'
    })

   new Vue({
       el: '#root',
       data: {
       }
   })

</script>

</body>
```



### 局部组件

```html
<body>
<div id="root">
    <aaa></aaa>
    <b-bb></b-bb>
</div>

<script>
    // 局部组件
    var aaa = {
        template: '<div>123123</div>'
    }
    var bbb = {
        template: '<div>123123</div>'
    }
    new Vue({
        el: '#root',
        // 组测子组件
        components: {
            aaa: aaa,
            BBb: bbb
        },
        data: {
        }
    })
</script>
</body>
</html>
```

### 组件间传值和props

### Vue生命周期

#### 什么是生命周期

#### 生命周期函数





## Vue项目开发流程

## 几个重要的Vue库


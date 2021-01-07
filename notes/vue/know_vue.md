# 认识VUE

## 一、MVVM模式

Model-View-View-Model模式：view和viewmodel的双向绑定

## 二、vue实例

``` js
# vue实例：app
var app = new Vue({
    el: '#app' // 指向能挂载的dom元素，可以是document.getElementById('id')
    data: { // data声明双向绑定的数据，此处声明的元素可以直接通过app.xxx访问

    }
})
```

### 2.1 生命周期：
- created：未挂载，$el还不可用
- mounted：el挂载上去之后调用
- beforeDestroy：实例销毁前

### 2.2 过滤器

{{ }} 表达式后面可以加 | 做数据过滤，指向过滤函数

``` javascript
<div id='app'>{{ date | formatData | formatData2('arg') }}</div>

```

### 2.3 指令

v-前缀，根据表达式的值应用相应的动作

- v-bind：动态更新html元素的属性，包括id、class等
- v-on：绑定事件监听器

示例：
``` js
<div id="app">
    <a v-bind:href="url">link</a>
    <!-- 等同于 --><a :href="url">link</a>
    <button v-on:click="clsClick">button</button>
    <!-- 等同于 --><button @click=:clsClick">button</button>
<script>
    var app = new Vue({
        date: {
            url: 'xxxxxxx'
        }
        methods: {
            clsClick: function() {}
        }
    })
</script>
```

## 三、计算

计算属性即：表达式是逻辑复杂的语句，可以用函数去写在computed选项内，然后{{}}内调用表达式

```js
<script>
    var app = new Vue({
        computed: {
            value_xxx: function() {}
        }
    })
</script>
```

### 用法

1. 表达式写在{{}}中，然后逻辑写在computed中，可以直接function返回值(要带上括号)，也可以写get set方法，会自动调用
2. 计算属性有依赖缓存，依赖的数据发生变化才会重新取值

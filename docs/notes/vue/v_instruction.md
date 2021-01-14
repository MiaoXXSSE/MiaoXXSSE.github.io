# 指令-directive

## v-bind

动态更新HTML元素上的属性：

eg:

### 1. href/src等
`v-bind:href="url"`:等同于`:href="url"`:href属性与url变量关联，随数据变化动态渲染

### 2. class
a) `class="static" :class="{ 'active': isActive, "error": isError}"`:根据isActive属性，如果是true，则class是active

b) 如果条件太多时，可以用`:class="classes"`，然后在computed函数块中写 classes 方法，并返回class的key-value对，如下：
``` js
computed: {
    classes: function() {
        return {
            active: this.isActive,
            error: this.isError
        }
    }
}
```

c) 数组表示`:class="[isActive ? activeClass : '', isError]"`,相当于从data中获取isActive和isError对应的value作为class

### 3. style
内联样式

a)`:style="{ 'color': color, 'footSize: fontSize + 'px' }"`

b) 写在data或者computed域中
``` js
:style="styles"

styles: {
    color: 'red',
    fontSize: 14 + 'px'
}
```

## v-cloak
无作用，编译后删除

网速慢 vue.js 没有加载完之前的带vue语法的文本的显示，可以通过cloak处理掉【vue-router多组件路由加载时不需要这个了】

```js
<element v-cloak />

css:
[v-cloak] {
    display: none
}
```

## v-once
标记元素/组件及子节点只渲染一次，后续不再随数据双向刷新 => 静态内容
`<element v-once />`

## v-if
处于效率会尽可能复用元素，可以用key使得不复用

``` js
# eg1:
<p v-if="status === 1">显示1</p>
<p v-else-if="status ===2">显示2</p>
<p v-else>显示</p>

# eg2:
<template v-if="status === 1>
    ......
</template>
```

## v-show
用来控制css的display属性，用法类似v-if，表达式为真时显示元素

- v-if：适用条件不经常改变的场景，切换开销较大
- v-show：适用频繁切换的条件

## v-for
遍历显示，用在循环元素或template标签中

books可以是computed块中的function，返回数组

`<li v-for="(book, index) in books">{{ index }} - {{ book.name }}</li>`

1. 能触发视图刷新的数组方法：push、pop、shift、unshift、splice、sort、reverse -> 修改了原数组
2. filter、concat、slice方法没有改变原数组，不会出发视图刷新

``` js
# eg：set索引触发刷新
Vue.set(app.books, 3, {
    name: 'asdf',
    author: 'adf'
});

# webpack中（没有导入vue）
this.$set(app.books,......)

# 另外的方法
app.books.slice(3, 1, {
    ......
})
```

## v-on

语法糖：`v-on:click="functionName"` -> `@click='count++'`

访问原生DOM事件：`@click="handleClient($event)"` -> $event变量

修饰符支持如下：
![修饰符](../../images/vue/修饰符.png)

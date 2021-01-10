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
## 

## v-once
标记元素/组件及子节点只渲染一次，后续不再随数据双向刷新 => 静态内容
`<element v-once />`

## 
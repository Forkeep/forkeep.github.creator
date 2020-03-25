---
title: "Vue中的.sync修饰符"
date: 2020-03-25T23:16:37+08:00
draft: true
---

## 前情提要

### Vue的一些规则

- 组件不能修改外部的props的数据
- $emit()可以触发事件并且传参
- $event 可以获得$emit的参数
- 上述为发布和订阅模式



### 场景

组件A传参给组件B，这个参数称之为money，组件B想要修改money的值，如果在组件B内直接修改这个props，则在组件A渲染时不奏效，会按照组件A之前的money值渲染，所以为了解决这个问题，我们怎么办？



### 基本解法

```vue
//App.vue
<template>
  <div class="app">
    App.vue 我现在有 {{total}}
    <hr>
    <Child :money="total" v-on:update:money="total = $event"/>
  </div>
</template>

<script>
import Child from "./Child.vue";
export default {
  data() {
    return { total: 10000 };
  },
  components: { Child: Child }
};
</script>

<style>
.app {
  border: 3px solid red;
  padding: 10px;
}
</style>

```



```vue
//Child.vue
<template>
  <div class="child">
    {{money}}
    <button @click="$emit('update:money', money-100)">
      <span>花钱</span>
    </button>
  </div>
</template>

<script>
export default {
  props: ["money"]
};
</script>


<style>
.child {
  border: 3px solid green;
}
</style>
```



> 实现效果：Child组件的button点击一下money会 -10 ，并且把值传递给App组件中。

- 初识状态：

![截屏2020-03-25下午11.08.56.png](https://i.loli.net/2020/03/25/u74pIyJMQxYzXwk.png)

- 点击一次后效果

![截屏2020-03-25下午11.09.37.png](https://i.loli.net/2020/03/25/198w7BEp5KsS4bH.png)



### 观察代码

```vue
// App.vue
<Child :money="total" v-on:update:money="total = $event"/>

// Child.vue
<button @click="$emit('update:money', money-100)">

```



因为这些操作过于常见，尤大干脆就简化了操作，给我们看了**一颗糖.sync**

```vue
// App.vue
<Child :money.sync="total" />//添加了.sync修饰符，等价于上边那些
// Child.vue
<button @click="$emit('update:money', money-100)">
```

所以，这就是.sync的含义和用法，我觉得拿实际例子讲，会比一些概念更清晰易懂~

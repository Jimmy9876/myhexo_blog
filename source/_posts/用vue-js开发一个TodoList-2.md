---
title: 用vue.js开发一个TodoList(2)
copyright: true
date: 2017-05-29 12:43:54
tags: vue.js
---

上次搭建完了环境，这次开始学习如何写一个TodoList。

首先打开文件

![](https://ws2.sinaimg.cn/large/006tNc79gy1fg24w7vy6cj305704o0sw.jpg)

`Hello.vue`

打开之后，删除`<template>`  ,`<script>` 内的与`HelloWorld`相关的代码。

之后，在文件中写入代码

```vue
<template>
  <div class="hello">
    <h1 v-text="title"></h1>
      <ul>
        <li v-for="item in items" v-bind:class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">
          {{ item.label }}
        </li>
      </ul>
  </div>
</template>

<script>
export default {
  data () {
    return {
      title: 'This is a todolist.',
      items: [
        {
          label: 'coding',
          isFinished: false
        },
        {
          label: 'walking',
          isFinished: true
        }
      ],
      liClass: 'ThisisliClass'
    }
  },
  methods: {
    toggleFinish: function (item) {
      item.isFinished = !item.isFinished
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.finished{
  text-decoration: underline;
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>

```

其中

```Vue
 <li v-for="item in items" v-bind:class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">
          {{ item.label }}
        </li>
```

`vue-for`用来渲染items里面的内容，items是一个数组，用来存放待完成的任务以及是否完成，里面的`vue-on`是绑定事件，绑定了一个click事件，点击即触发，触发的方法是method里面的function，这个function实现了点击去除下划线的功能。

接下来使用v-model实现一个双向绑定，构建一个input输入框，实现输入按回车就能将数据存放到数组里展示到页面上

```Vue
 <input v-model="newItem" @keyup.enter="addNew">

<script>
export default {
  data () {
    return {
      title: 'This is a todolist.',
      items: [
      ],
      newItem: ''
    }
  },
  methods: {
    toggleFinish: function (item) {
      item.isFinished = !item.isFinished
    },
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isFinished: false
      })
      this.newItem = ''
    }
  }
}
</script>
```

具体项目源码已上传至[github](https://github.com/Jimmy9876/TodoList)

至此实现了一个简单的todolist。

![](https://ws3.sinaimg.cn/large/006tNc79gy1fg25pjbu7nj30at0emaab.jpg)

#  



# 未完待续...


---
title: 用vue.js开发一个TodoList(3)
copyright: true
date: 2017-05-29 20:55:16
tags: vue.js
---

> 前两次开发的没有加入存储功能，一刷新页面，todolist也会随之消失

为了让todolist刷新页面仍然存在于页面中，这里用到localstorage。

下面是代码:

文件`Hello.vue`



```
<template>
  <div id="app">
    <h1 v-html="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew"></input>
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinish(item)">{{item.label}}</li>
    </ul>
  </div>
</template>

<script>
import Store from './store'
export default {
  data: function () {
    return {
      title: 'This Is A Todolist',
      items: Store.fetch(),
      newItem: ''
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
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

<style>
.finished {
  text-decoration: underline;
}

li {
  list-style: none;
  font-size: 1.6em;
  margin-top: 10px;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

input {
  width: 230px;
  height: 40px;
  border-radius: 20px;
  padding: 0.4em 0.35em;
  border: 3px solid #CFCFCF;
  font-size: 1.55em;
}
</style>
```

文件`store.js`

```javascript
const STORAGE_KEY = 'todos-vuejs'
export default {
  fetch: function () {
    return JSON.parse(window.localStorage.getItem(STORAGE_KEY) || '[]')
  },
  save: function (items) {
    window.localStorage.setItem(STORAGE_KEY, JSON.stringify(items))
  }
}

```

两个方法：一个设置，一个获取，将两个方法加入到`Hello.vue`中去,代码已放到[github](https://github.com/Jimmy9876/TodoList)欢迎持续关注，如有问题欢迎留言交流
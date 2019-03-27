---
title: vuex
date: 
tags:
- vue
categories: 
- web前端
---
## 初步认识
> 你理或者不理她都在那里管理所有组件状态的贴心共享小仓库，直到有天你对她有了好奇心。

- 使用场景  
> 当组件之间的通信过于繁琐、耦性太强的时候使用。  

 举个栗子：  
 一个Vue的根实例下面有一个根组件名为**App.vue**, 它下面有两个子组件**A.vue**和**B.vue**, **App.vue**想要与**A.vue**或者**B.vue**通讯可以通过props传值的方式, 但是如果A.vue和B.vue之间的通讯就很麻烦了, 他们需要共有的父组件通过自定义事件进行实现, A组件想要和B组件通讯往往是这样的：
 ![](/vuex1/20190328121820048.png)
 - A组件说: "报告老大, 能否帮我托个信给小弟B" => dispatch一个事件给App
 - App老大说: "包在我身上, 它需要监听A组件的dispatch的时间, 同时需要broadcast一个事件给B组件"
 - B小弟说: "信息已收到", 它需要on监听App组件分发的事件
 
 ## 碰撞火花  
     1.下载 **vuex**: **npm install vuex --save**  
     2.在 **main.js** 添加:
     ```
     import Vuex from 'vuex'

     Vue.use( Vuex );

     const store = new Vuex.Store({
         //待添加
     })

     new Vue({
         el: '#app',
         store,
         render: h => h(App)
     })
```  
## 地上摩擦
 
 
 
 
 
 
 
 
 
 
 
 
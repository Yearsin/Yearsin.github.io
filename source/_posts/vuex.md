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

> 当组件之间的通信过于繁琐、耦性太强的时候使用。  

 举个栗子：  
 一个Vue的根实例下面有一个根组件名为**App.vue**, 它下面有两个子组件**A.vue**和**B.vue**, **App.vue**想要与**A.vue**或者**B.vue**通讯可以通过props传值的方式, 但是如果A.vue和B.vue之间的通讯就很麻烦了, 他们需要共有的父组件通过自定义事件进行实现, A组件想要和B组件通讯往往是这样的：
![](../../public/images/vuex-img-1.png)
 - A组件说: "报告老大, 能否帮我托个信给小弟B" => dispatch一个事件给App
 - App老大说: "包在我身上, 它需要监听A组件的dispatch的时间, 同时需要broadcast一个事件给B组件"
 - B小弟说: "信息已收到", 它需要on监听App组件分发的事件
 
## 碰撞火花  
 1.下载 **vuex**: **npm install vuex --save**  
 2.本文demo做了抽离处理。
 3.(常规)在 **main.js** 添加:
     
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
用代码示例来讲话，我使用 **vue-cli** 初始化了一个demo，**[master分支](https://github.com/Yearsin/vue-demo)**进行下载，node.js版本8.11.3。
![](../../public/images/vuex-img-2.png)
![](../../public/images/vuex-img-3.png)
 
- State:
我把她看做是所有组件的 **data**，用于保存所有组件公共的数据。
```
const state = {
    empirical: 0 // 经验值
};
```

- Getters
**store** 的 **computed** 也就是计算属性，接受 **state** 作为其第一个参数，也可以接受其他 **getter** 作为第二个参数。
定义:  
```
const getters = {
    empirical: state => {
        return state.empirical;
    }
};
```
    获取:
```
this.$store.state.mutations.empirical
```

- Mutations  
1.用于同步操作。
2.**store** 中的 **methods**，是改变状态的唯一方法。
3.该函数名官方规定叫 **type**，第一个参数是state，第二参数是**payload**，也就是自定义的参数。
定义:
```
const mutations = {
    setEmpirical (state, data) {
        state.empirical = data;
    }
};
```
    提交:
```
this.$store.commit('setEmpirical', this.$store.state.mutations.empirical);
```
- Actions  
1.用于异步操作。
2.类似 **mutations**。
3.**actions** 提交的是 **mutations** 而不是直接变更状态。
4.**actions** 中的回调函数的第一个参数是 **context**， 是一个与 **store** 实例具有相同属性和方法的对象。
定义:
```
    setEmpiricalAsync: (context) => {
        setTimeout(() => {
            context.commit('setEmpirical', 10); // context提交
        }, 2000);
    }
```
    提交:
```
this.$store.dispatch('setEmpiricalAsync');
```
- Modules
应用复杂时，**module** 使 **store** 对象看起来不太丑陋。
> 由于使用单一状态树，应用的所有状态会集中到一个比较大的对象。当应用变得非常复杂时，store 对象就有可能变得相当臃肿。为了解决以上问题，Vuex 允许我们将 store 分割成模块（module）。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割。

    ```
import Vue from 'vue';
import Vuex from 'vuex';
import actions from './actions.js';
import mutations from './mutations.js';

Vue.use(Vuex);

export default new Vuex.Store({
    modules: {
        mutations
    },
    actions
});
```
 
 
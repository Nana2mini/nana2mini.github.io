---
layout: post
title:  "Vue 使用一点总结"
date:   2018-05-10 21:06:04
categories: jekyll update
---

一个切图仔日常开发中使用过的一些Vuejs技巧

<!-- more -->

**1.重新赋值**

从index位置删除n个元素，并向其添加val元素

{% highlight ruby %}
Array.splice(index, n, val);    
this.$set(this.items, indexOfItem, newValue)
Object.assign(target, ...sources)
{% endhighlight %}



**2.使用全局变量**

将store中的getter映射到局部计算属性中
{% highlight ruby %}
computed: {
    ...mapGetters(['fields'])
}
{% endhighlight %}
    
  
**3.解决刷新或者加载页面出现{{message}}**

{% highlight ruby %}
<style type="text/css">	
  [v-cloak]{
      display:none;
  }
</style>
{% endhighlight %}
    

**4.父子组件通信**


***parent.vue***
{% highlight ruby %}

<template>
    <div>
        <button v-on:click="parentClick">点击</button>
        <child-component ref="childComponent" @toParent="handleChildClick"></child-component>
    </div>
</template>
<script>
    import ChildComponent from './childComponent';
    export default {
        name: "parent",
        components: {
            ChildComponent
        },
        methods: {
            parentClick() {
            // 调用子组件方法
            this.$refs.childComponent.handleParentClick("Hello World");
            }
            handleChildClick(val) {
            // val是从子组件传过来的
            handleChildClick

            }
        }
    }
</script>
{% endhighlight %}


***child.vue***

{% highlight ruby %}
<template>
    <div>
    <button v-on:click="childClick">点击</button>
    </div>
</template>
<script>
    export default {
        name: "childComponent",
        methods: {
            handleParentClick(val) {
            // val是从父组件传过来的
            console.log(val)
            },
            childClick(pars) {
                this.$emit('toParent', '子组件传值给父组件')
            }
        }
    }
</script>
{% endhighlight %}

**5.要在DOM更新以后再执行某一块代码，把这块代码放到下一次事件循环里面**

{% highlight ruby %}
this.$nextTick(function() {
  // Todo
})
{% endhighlight %}

**6.类型转换优化级**

{% highlight ruby %}
// 转数字
var status = '1';
// (+status) > Number(status) > Math.round(status) > parseInt(status)

// 转字符串
var status = 1;
// (''+status) > String(status) > status.toString() > new String(status）
{% endhighlight %}

    
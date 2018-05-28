## Vue1 与 Vue2的不同

>   不能拿body与html定义作用域

>   vue2 不需要过滤器就可以解析json

>   生命周期：
    created
    beforeCompile
    compiled
    ready
    beforeDestroy
    destroyed


    新增：beforeCreate=》实例创建开始 属性还未绑定
    created
    beforeMount   渲染之前
    mounted  数据渲染完了 //相当于ready
    beforeUpdate
    updated
    beforeDestroy
    destroyed

>   循环中$index、$key没了 

        v-for((val,index)in arr) 2里边val是第一个参数，1里边index是第一个

>   过滤器

    2里边所有的自带过滤器都没了 但是自定义过滤器还是一样的 除了传参
    1=>uppercase "1" "2"
    2=> uppercase("1","2")
 
>   组件

    2.0<template>标签下必须要有且只有一个根元素

    父子组件数据同步

    1=>:vriable.sync(在子组件的自定义属性上加上.sync)
    2=> 如果父级传对象 如果想同步 直接根据js的对象引用自动就会同步
        如果父级传对象，还不想同步，那么只能在子组件data里定义新变量，在mounted里边给新变量赋值（让赋值变量不是对象就好）

    父子组件数据传递

    1:父=》子 props
    子=》父 emit
    同级：emit=》props 子到父 =》 父到子

    2:vm = new Vue();
    new Vue({

    })
    vm.$emit(key,value)
    vm.$on(key,function(data){//data即为emit中的value})

>   动画-----也是有生命周期的

    <transition name="fade">
        <div v-show="show">
        </div>
        要运动的元素
    </transition>

    fade-enter进入之前
    fade-enter-active进入

    fade-leave消失之前
    fade-leave-active消失

    transition-group    

>   路由

    1：<a v-link='{path:""}'>
    2:<router-link to=""></router-link>



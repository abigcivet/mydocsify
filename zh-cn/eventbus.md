# bus事件总线

>`bus`事件总线是vue自带的一种组件间传值的方式

```bash

    import Vue from 'vue'   // bus是基于vue的 把vue引入

    export const eventBus = {};  // 导出一个对象  对象用于存放标记
    eventBus.bus = new Vue();  // 实例化一个bus

    eventBus.ADD = 'ADD';  //  标记

    /*
       例子:
       eventBus.bus.$emit(eventBus.ADD,this.msg);        发送事件监听  this.msg是要传入的参数 可以是一个{}

       eventBus.bus.$on(eventBus.ADD,this.changeTwo);    接收事件接听  this.changeTwo是一个要执行的函数

       eventBus.bus.$off(eventBus.ADD,this.changeTwo);   移除事件监听  this.changeTwo是一个要执行的函数
    */

```
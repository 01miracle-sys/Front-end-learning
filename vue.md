## vue2+vue3

Vue:用于构建用户界面的渐进式js框架 （简单应用：只需一个清凉小巧的核心库）

1.组件化

2.声明式

3.使用虚拟DOM和优秀的DIff算法，尽量复用DOM节点

**注意区分：js表达式 和js代码（语句）**

1.表达式：



### Vue中有两种数据绑定方式：

1.v-bind 单向绑定，数据只能从data流向页面  ：

2.v-model双向绑定，数据不仅能从data流向页面，还可以从页面流向data，一般用于表单类元素上（如input、select等）

v-model：value 可以简写为v-model，因为v-model默认收集的就是value值

el的两种写法：

1.el：‘#root’， .new Vue时配置el属性

2.v.$mount（‘#root’）  先创建Vue实例，随后再通过vm.$mount('#root')指定el的值

data的两种写法：

1.对象式 data：{name：‘  ’}

2.函数式 data：function（）{ return{name：‘  ’}}  后续学习组件时，data必须用函数式，否则会报错

由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例

### MVVM模型：

1.M模型（model）：对应data中的数据

2.V试图（View） 模板

3.VM视图模型（ViewModel） Vue实例对象

### object.defineProperty方法

object.defineProperty(): 静态方法会直接在一个对象上定义一个新属性，或修改其现有属性，并返回此对象。

enumerable:true ，控制属性是否可以枚举，默认值是false

writeable：true， 控制属性是否可以被修改，默认值是false

configurable：true ，控制属性是否可以被删除，默认值是false



读取xxx的xx属性时，get函数（getter）就会被调用，且返回值就是xx的值

getter：get+函数 属性值+函数值

修改xxx的xx属性时，set函数（setter）就会被调用，且返回值就是xx的值

set

### 数据代理

通过一个对象代理对另一个对象中属性的操作（读/写）

![image-20260105213651024](.\img\image-20260105213651024.png)

### 事件处理

v-on:click  @click

methods：{ showInfo（）{alert（‘’）}

}

事件的基本使用：1.使用v-on：xxx或@xxx 绑定事件，其中xxx是事件名；

2.事件的回调需要配置在methods对象中，最终会在vm上；

3.methods中配置的函数，不要用箭头函数，否则this就不是vm了

4.methods中配置的函数，都是被Vue所管理的函数，this的指向是vm 或组件实例对象；

5.@click=“demo” 和@click=“demo（$event）”效果一致，但后者可以传参；

vue中的事件修饰符：

1.prevent：阻止默认事件（常用）

2.stop：阻止事件冒泡（常用）

3.once：事件只触发一次（常用）

4.capture：使用事件的捕获模式；

5.self：只有event。target是当前操作的元素是才触发事件；

6.passive：事件的默认行为立即执行，无需等待事件回调执行完毕；





















## vue3

一个.vue文件里面包含三个标签

<template>
    html  结构
</template>


<script lang='ts'>
    js或者TS    vue3推荐使用ts来写 交互
</script>


<style>
    样式
</style>

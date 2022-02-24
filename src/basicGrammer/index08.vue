<template>
    <!-- 十一、API的配置使用 -->
    <!-- 1、应用配置 -->
    <!-- 
        app.config.errorHandler = (err, vm, info) => {
    // 处理错误
    // `info` 是 Vue 特定的错误信息，比如错误所在的生命周期钩子
    } -->
    <!-- 
        app.config.warnHandler = function(msg, vm, trace) {
        // `trace` 是组件的继承关系追踪
        }
     -->
    <!-- globalProperties： 添加一个可以在应用的任何的实例中访问全局的property;
    组件的property在命名冲突时具有优先权
    app.config.globalProperties.foo = 'bar'
    app.component('child-component', {
    mounted() {
        console.log(this.foo) // 'bar'
    }
    }) -->
    <!-- performace: boolean在开发模式下，开启浏览器对性能进行跟踪 -->
    <!-- compilerOptions:配置运行时编译器的选项 -->
    <!-- 2、应用API -->
    <!-- component方法：
    import { createApp } from 'vue'
    const app = createApp({})
    // 注册一个选项对象
    app.component('my-component', {
    /* ... */
    }) -->
    <!-- config: 配置对象
    import { createApp } from 'vue'
    const app = createApp({})
    app.config = {...} -->
    <!-- directive： 注册和检索全局的指令
    // 注册
    app.directive('my-directive', {
    // 指令具有一组生命周期钩子：
    // 在绑定元素的 attribute 或事件监听器被应用之前调用
    created() {},
    // 在绑定元素的父组件挂载之前调用
    beforeMount() {},
    // 在绑定元素的父组件挂载之后调用
    mounted() {},
    // 在包含组件的 VNode 更新之前调用
    beforeUpdate() {},
    // 在包含组件的 VNode 及其子组件的 VNode 更新之后调用
    updated() {},
    // 在绑定元素的父组件卸载之前调用
    beforeUnmount() {},
    // 在绑定元素的父组件卸载之后调用
    unmounted() {}
    }) -->
    <!-- el: 指令绑定到元素，这可用于直接操作dom -->
    <!-- 十二、全局API -->
    <!-- const { createApp, h, nextTick } = Vue
    import { createApp, h, nextTick } from 'vue'
     -->
    <!-- 1、createApp：返回一个提供上下文的应用实例 -->
    <!-- 2、h: 返回一个虚拟的节点；
     render() {
        return h('h1', {}, 'Some title')
    }
    接口三个参数：type：HTML 标签名、组件、异步组件或函数式组件。
    props：一个对象与我们在模版中使用的attribute，prop和事件相对应
    children：子代 VNode，使用 h() 生成，或者使用字符串来获取“文本 VNode”，或带有插槽的对象。可选。
     -->
    <!-- defineComponent：从实现上看，defineComponent 只返回传递给它的对象。从类型来看是返回一个合成类型的构造函数 -->
    <!-- defineAsyncComponent：创建一个需要时才加载的异步组件；
    基本用法：可以接受一个返回 Promise 的工厂函数；Promise 的 resolve 回调应该在服务端返回组件定义后被调用。
    你也可以调用 reject(reason) 来表示加载失败。 -->
    <!-- defineCustomElement： 和defineComponent接收相同的参数，返回一个自定义的元素 -->
    <!-- nextTick：将回调推迟到下一个 DOM 更新周期之后执行。在更改了一些数据以等待 DOM 更新后立即使用它。 -->
    <!-- 十三、选项 -->
    <!-- 1、data: 该函数返回组件实例的data对象，
    在 data 中，我们不建议观察具有自身状态行为的对象，如浏览器 API 对象和原型 property。一个好主意是这里只有一个表示组件 data 的普通对象。
    需要深入了解响应性原理 -->
    <!-- 2、prop： 可以接收数组和对象，对象中的type，require，default, validator -->
    <!-- 3、computed：计算属性将被混入到组件实例中。所有 getter 和 setter 的 this 上下文自动地绑定为组件实例。
    注意：如果使用了箭头函数，则this不会指向这个实例 -->
    <!-- 4、methods: 将被混入到组件实例中。可以直接通过 VM 实例访问这些方法，或者在指令表达式中使用。方法中的 this 自动绑定为组件实例。 -->
    <!-- 5、watch方法：一个对象，键是要侦听的响应式 property——包含了 data 或 computed property，而值是对应的回调函数。值也可以是方法名，或者包含额外选项的对象 -->
    <!-- 6、emits：可以是数组或者对象从组件触发自定义事件，emits 可以是简单的数组，也可以是对象，后者允许配置事件验证。 -->
    <!-- 7、expose：一个将暴露在公共组件实例上的 property 列表。 -->
    <!-- 8、DOM:template一个字符串模版，用作component实例的标记，模版将替换所挂载元素的innerHTML -->
    <!-- 9、render函数，字符串模版之外的另一种选择，允许你充分利用javascript功能 -->
    <!-- const { createApp, h } = Vue
        const app = createApp({})
        app.component('my-title', {
        render() {
            return h(
            'h1',           // 标签名称
            this.blogTitle  // 标签内容
            )
        },
        props: {
            blogTitle: {
            type: String,
            required: true
            }
        }
        })

        app.mount('#app') -->
    <!-- 十四、生命周期钩子函数 -->
    <!-- 所有的生命周期钩子函数中的this的上下文都自动绑定到实例中 -->
    <!-- beforeCreate：实例初始化之后、进行数据侦听和事件/侦听器的配置 -->
    <!-- created: 实例创建之后被立即同步调用, 在这一步实例中已经完成对选项的处理-->
    <!-- beforeMounted: 在挂在之前调用，相关的 render 函数首次被调用。 -->
    <!-- mounted：在挂在之后调用，注意mounted不会保证所有的子组件都挂载完成，如果希望整个视图都渲染完成
    可以在mounted内部使用vm.$nextTick -->
    <!-- beforeUpdate:数据发生改变后，DOM被更新之前调用 -->
    <!-- updated:在数据更改导致的虚拟 DOM 重新渲染和更新完毕之后被调用。
    所以可以执行依赖于DOM的操作，然而大多数情况下，应该避免在这个状态下更改状态。如果要相应状态改变，通常最好使用计算属性或侦听器取而代之。
    意，updated 不会保证所有的子组件也都被重新渲染完毕。如果你希望等待整个视图都渲染完毕，可以在 updated 内部使用 vm.$nextTick：
     -->
    <!-- activated：被 keep-alive 缓存的组件激活时调用。 -->
    <!-- deactivated： 被 keep-alive 缓存的组件失活时调用。 -->
    <!-- beforeUnmount：在卸载实例之前调用 -->
    <!-- unmounted: 卸载组件实例之后调用，调用此钩子函数时，组件实例的所有指令
    都被解除绑定 -->
    <!-- 十五、选项/资源 -->
    <!-- 1、directives:指令 -->
    <!-- 2、components： 组件 -->
    <!-- 3、mixins：接收一个mixin对象的数组 -->
    <!-- 4、extends:允许一个组件扩展到另一个组件，且继承这个组件的选项 -->
    <!-- 5、provide / inject -->
    <!-- 6、setup： 函数是一个新的组件选项，它是组件内部使用组合api的入口点 
    调用时间：在创建组件实例时，，在初始 prop 解析之后立即调用 setup。在生命周期方面，它是在 beforeCreate 钩子之前调用的。
    -->
    <!-- 十六、实例property -->
    <!-- $data: 组件实例正在侦听的数据对象，组件实例代理了对其data对象property的访问 -->
    <!-- $props: 当前组件接收到的props，组件实例代理了对其props对象property的访问  -->
    <!-- $el: 组件实例正在使用的根 DOM 元素。 -->
    <!-- $options: 用于当前组件实例的初始化选项。当你需要在选项中包含自定义 property 时会有用处： -->
    <!-- $parent: 父实例，如果当前实例有的话。 -->
    <!-- $root: 当前组件树的根组件实例。如果当前实例没有父实例，此实例将会是其自己。 -->
    <!-- $slots: 用来以编程方式访问通过插槽分发的内容。每个具名插槽都有其相应的 property
     (例如：v-slot:foo 中的内容将会在 this.$slots.foo() 中被找到)。default property 包括了所有没有被包含在具名插槽中的节点，或 v-slot:default 的内容。 -->
     <!-- $refs：一个对象，持有注册过 ref attribute 的所有 DOM 元素和组件实例。 -->
     <!-- $attrs： 包含了父作用域中不作为组件 props 或自定义事件的 attribute 绑定和事件。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定，并且可以通过 v-bind="$attrs" 传入内部组件——这在创建高阶的组件时会非常有用。 -->
     <!-- 十七、实例方法 -->
     <!-- 1、$watch方法，侦听组件实例上的响应式的property或函数计算结果的变化，
      当监听的是一个数组或者对象的时候，不会触发$watch；
      通过deep去解决这个问题，immediate表示立即执行回调函数-->
     <!-- 
      2、 $emit方法：触发一个事件
      -->
      <!-- 3、$forceUpdate：迫使组件实例重新渲染，注意它仅仅影响实例本身和插入插槽内容的子组件，而不是所有子组件。 -->
      <!-- 4、$nextTick -->
      <!-- 十八、指令 -->
      <!-- 1、v-text： -->
      <!-- 2、v-html -->
      <!-- 3、v-show -->
      <!-- 4、v-if -->
      <!-- 5、v-else -->
      <!-- 6、v-for -->
      <!-- 7、v-on -->
      <!-- 8、v-bind -->
      <!-- 9、v-model -->
      <!-- 10、v-slot -->
      <!-- 十九、特殊的attribute -->
      <!-- 1、key -->
      <!-- 2、ref -->
      <!-- 3、is -->
      <!-- 二十、内置组件 -->
      <!-- 1、keep-live -->
      <!-- 2、transition -->
      <!-- 3、 transition-group-->
      <!-- 4、component is 动态加载组件 -->
      <!-- 5、slot -->
      <!-- 6、 teleport-->
      <!-- 二十一、响应性基础API -->
      <!-- 1、reactive -->
      <!-- 2、readonly -->
      <!-- 3、isProxy -->
      <!-- 4、isReactive -->
      <!-- 5、isReactive -->

</template>
<script>
export default {
    watch: {
        // 侦听顶级的property
        a(newValue, oldValue) {
            console.log(`new: ${val}, old: ${oldVal}`)
        },
        // 字符串方法名
        b: 'someMethod',
        // 该回调会在任何被侦听的对象的 property 改变时被调用，不论其被嵌套多深
        c: {
            handler(newValue, oldValue) {
                console.log('c changed');
            },
            deep: true
        },
        // 侦听单个嵌套的property
        'c.d': function(newValue,oldVlaue) {
            console.log(newValue);
        },
        // 该回调将会在侦听之后，立即调用
        'e': {
            handler(newValue, oldValue) {
                console.log(newValue);
            },
            immediate: true,
        },
        // 也可以传入回调数组，它们会被逐一调用
        'f': [
            'handle1',
            function handle2(newValue, oldValue) {
                console.log(newValue);
            },
            {
                handler(newValue, oldValue) {
                    console.log(newValue);
                }
            },

        ]
    },
    methods: {
        someMethod() {
          console.log('b changed')
        },
        handle1() {
          console.log('handle 1 triggered')
        }
    }
}
</script>
<style>
</style>

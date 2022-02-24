<template>
    <!-- 六、Provide / Inject-->
    <!-- 1、当父组件向子组件传递数据时，无论层级有多深，父组件都可以为子组件 -->
    <div>{{ user }}</div>
    <!-- 但是如果我们尝试在此处provide一些组件的实例property，这将是不起作用的 -->
    <!-- 这实际上时长距离的prop;父组件不需要知道prop在哪个组件使用，子组件也不需要知道prop来自哪里 -->
    <!-- 2、处理响应 -->
    <!-- 如果我们更改了todos列表，这种响应不会 inject 的 todoLength中 -->
    <!-- 七、动态组件和异步组件 -->
    <!-- 失活的组件将会被缓存！-->
    <keep-alive>
        <component :is="currentTabComponent"></component>
    </keep-alive>
    <!-- 异步组件 defineAsyncComponent定义一个异步的组件，同时可以和suspense一起使用-->
    <!-- 八、模版引用 -->
    <!-- 通过ref可以直接访问子组件 -->
    <input ref="input" placeholder="你好测试"/>
    <!-- this.$refs只会在组件渲染完成之后生效，应该避免在模版或计算属性中使用 -->
    <!-- 九、处理边界情况 -->
    <!-- 1、控制更新中的强制更新 $forceUpdate -->
    <!-- 2、低级静态组件与 v-once，可以通过v-once对于一些静态组件，进行缓存 -->
</template>
<script>
import {computed } from 'vue'
export default {
    inject: ['user'],
    data() {
        return {
            todos: ['Feed a cat', 'Buy tickets']
        }
    },
    // provide: {
        // 这种方式将会报错
        // todoLength: this.todos.length 
    // },
    provide() {
        return {
            // todoLength: this.todos.length,
            // 进行响应的
            todoLength: computed(() => this.todos.length)
        }
    },
    created() {
       console.log(`Injected property: ${this.user}`) // > 注入的 property: John Doe
    },
    methods: {
        focusInput() {
            console.log(this.$refs.input.focus);
            this.$refs.input.focus()
        }
    },
    mounted() {
        this.focusInput()
    }
}
</script>
<style>
</style>

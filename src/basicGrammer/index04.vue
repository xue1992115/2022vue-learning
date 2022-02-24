<template>
    <!-- 四、组件的基础 -->
    <!-- 1、组件是带有名称可以复用的实例，和根实例一样，接受相同的data和生命周期函数；
    组件复用中，每使用一次组件，就会有一个新的实例被创建 -->
    <!-- 父子组件的通讯，父组件->子组件 通过props的方式进行通讯；父组件监听子组件的方法，子组件$emit一个方法"$emit('enlargeText', 0.1)" -->
    <!-- 2、在自定义的组件上使用v-model -->
    <!-- 将其 value attribute 绑定到一个名叫 modelValue 的 prop 上 -->
    <!-- 在其 input 事件被触发时，将新的值通过自定义的 update:modelValue 事件抛出 -->
    <!-- 
    app.component('custom-input', {
    props: ['modelValue'],
    emits: ['update:modelValue'],
    template: `
        <input
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        >
    `
    })
    <custom-input v-model="searchText"></custom-input>
     -->
    <!-- 3、按照插槽分发内容 -->
    <!-- 4、动态组件的使用 -->
    <!-- 组件会在 `currentTabComponent` 改变时改变 -->
    <component :is="currentTabComponent"></component>
    <!-- 5、组件注册：全局的注册和局部的注册 -->
    <!-- 全局注册：Vue.createApp({...}).component('my-component-name', {
    // ... 选项 ...})
    全局注册组件之后，可以用在任何新创建的组件实例当中 -->
    <!-- 局部注册： -->
    <!-- 6、Props类型 -->
    <!-- 以字符串数组的形式：props: ['title', 'likes', 'isPublished', 'commentIds', 'author'] -->
    <!-- 对象的形式 -->
    <!-- prop的验证 -->
    <!-- 7、自定义事件 -->
</template>
<script>
export default {
    data() {
        return {

        }
    },
    props: {
        // 基础类型的检查，(null和undefined会通过所有类型的检查)
        propsA: Number,
        propB: [String, Number],
        // 必填的字符串
        propC: {
            type: String,
            required: true
        },
        // 带有默认值的数字
        propD: {
            type: Number,
            default: 100
        },
        // 带有默认值的对象
        propE: {
            type: Object,
            // 对象或数组的默认值必须从一个工厂函数返回
            default() {
                return { message: 'hello' }
            }
        },
         // 自定义验证函数
        propF: {
            validator(value) {
                // 这个值必须与下列字符串中的其中一个相匹配
                return ['success', 'warning', 'danger'].includes(value)
            }
        },
        // 具有默认值的函数
        propG: {
            type: Function,
            // 与对象或数组的默认值不同，这不是一个工厂函数——这是一个用作默认值的函数
            default() {
                return 'Default function'
            }
        }
    }
}
</script>
<style>
</style>

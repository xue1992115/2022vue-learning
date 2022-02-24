<template>
    <div>
        <!-- 五、插槽 -->
        <!-- 插槽是内容分发的API,将slot元素作为承载内容分发的出口 -->
        <button class="btn-primary">
            <!-- slot中的字段为备用的内容,如果父组件分发内容了，则内用内容不显示 -->
            <slot>submit</slot>
        </button>
        <!-- 父级模版中的所有内容都是在父级作用域中编译的；子模版中的所有内容都是在子作用域中编译的 -->
        <!-- 1、具名插槽 -->
        <!-- 注意：在父组件上，v-slot只能添加到template上
        如：<template v-slot:header></template>,只有一种情况例外，就是我们可以使用在组件上，参考3 -->
        <div class="container">
            <slot name="header"></slot>
            <slot></slot>
            <slot name="footer"></slot>
        </div>
    </div>
    <!-- 2、作用域插槽： 就是让父组件可以访问子组件中的内容 -->
    <!-- 作用域插槽就是子组件中的slot中，将数据通过arttribute的方式绑定
    父组件中通过slotProps去获取 -->
    <!-- <ul>
        <li v-for="(item, index) in items">
            <slot :item="item"></slot>
        </li>
    </ul> -->
    <!-- <todo-list>
        <template v-slot:default="slotProps">
            <i class="fas fa-check"></i>
            <span class="green">{{ slotProps.item }}</span>
        </template>
    </todo-list> -->
</template>
<script>
export default {
    data() {
        return {
            buttonText: 'buttonText'
        }
    }
}
</script>
<style>
</style>

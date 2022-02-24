<template>
    <!-- 二、Data Property和方法 -->
    <!-- 1、注意这些property仅在实例首次创建时被添加，所以需要确保它们都在data函数返回的对象中；
    直接将不包含在data中的property添加到组件实例中也是可行的，但是Vue的响应系统不会自动更新它 -->
    <div>{{ count }}</div>
    <div>{{ $data.count }}</div>
    <div>{{ person }}</div>
    <!-- 2、vue自动为methods绑定this,以便它始终指向组件实例;所以定义method时应避免使用箭头函数，因为这会阻止vue绑定正确的实例-->
    <!-- 3、防抖和节流函数，vue没有内置的函数，需要使用lodash库去实现 -->
    <!-- 这种方法对于复用的组件有潜在的问题，因为它们有相同的防抖函数，为了组件实例彼此独立
    可以在生命周期函数钩子函数created里添加该函数 -->
    <div @click="changeCountValue">{{ counter}}</div>
</template>
<script>
export default {
    data() {
        return {
            count: 4,
            counter: 0,
        }
    },
    mounted() {
        this.changNameValue();
        this.init()
    },
    created() {
         // 使用 Lodash 实现防抖
        this.debouncedClick = _.debounce(this.changeCountValue, 500)
    },
    unmounted() {
        // 移除组件时，取消定时器
        this.debouncedClick.cancel()
    },
    methods: {
        changNameValue() {
            // person不在响应系统中
            this.person = '哈哈哈哈哈'
        },
        // changeCountValue: _.debounce(function() {
        //     this.counter += 1;
        // }, 500),
        changeCountValue() {
            this.counter += 1;
        },
        init: () => {
            // console.log(this.count);
            // 因为是箭头函数，箭头函数时没有this的，因此要去methods中寻找
            // console.log(this.data);
        },
        // init(){
        //     // console.log(this.count);
        //     console.log(`this:${this.count}`);
        // },
    }
}
</script>
<style></style>

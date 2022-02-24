<template>
    <!-- 一、基础的语法 -->
    <!-- 1、文本插值 -->
    <div>{{ msg }}</div>
    <!-- 2、v-once指令，只能执行一次插值 -->
    <div v-once>{{ msg }}</div>
    <!-- 3、原始的html -->
    <div v-html="rawHtml"></div>
    <!-- 4、Attribute，通过v-bind指令动态的绑定属性，简写如下：
    如果绑定的值是null或undefined则不会渲染在dom元素上,同时可以绑定boolean值 -->
    <div v-bind:id="dynamicId">Attribute绑定</div>
    <div :id="dynamicId2">Attribute绑定简写</div>
    <button v-bind:disabled="isButtonDisabled">按钮</button>
    <!-- 5、javascript表达式的使用，每个绑定只能包含单个表达式，所以 -->
    <div>{{ number + 1 }}</div>
    <div>{{ ok ? 'YES' : 'NO' }}</div>
    <div v-bind:id="'number-' + number"></div>
    <!-- 这个列子不会生效 -->
    <!-- <div>{{ if (ok) { return message } }}</div> -->
    <!-- 6、指令，指令的作用就是，当表达式的值变化的时候，其产生的连带的影响，响应式的作用于dom -->
    <p v-if="seen">现在你看到我了</p>
    <!-- 7、指令可以接受一个参数 -->
    <a v-bind:href="url"> 指令接受参数 </a>
    <!-- 8、指令动态接受一个参数 -->
    <a v-bind:[attributeName]="url"> 指令接受参数 </a>
    <!-- 9、修饰符：用于指出一个指令应该以特殊的方式绑定 -->
    <!-- .prevent: 告诉v-on指令对于触发的事件，调用event.preventDefault()，阻止默认事件的调用-->
    <div v-on:click.prevent="onSubmit">修饰符：.prevent</div>
    <!-- .stop: 阻止事件的冒泡行为，@click是简写的行为-->
    <div @click.stop="onSubmit">修饰符：.prevent</div>
</template>
<script>
export default {
    data() {
        return {
            number: 0,
            msg: "hello world",
            rawHtml: '<span style="color: red">你好</span>',
            dynamicId: 1234,
            dynamicId2: undefined,
            isButtonDisabled: '',
            seen: false,
            url: 'https://baidu.com',
            attributeName: 'href',
            ok: 111,
        }
    },
    mounted() {
        setTimeout(() => {
            this.msg = '变更信息';
            this.seen = true;
        }, 1000)
    },
    methods: {
        onSubmit() {
            console.log('onSubmit');
        }
    }
}
</script>
<style></style>

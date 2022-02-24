<template>
<!-- 二十二、组合API的使用  -->
<!-- 1、setup函数：接收两个参数，props和context
props,正如一个标注组件期望的那样，setup函数中的props是响应式的；当传入新的prop,它将被更新；
因为props是响应式的，因此不能使用es6的解构方式去解构，它会消除props的响应性；
如果需要解构，可以在setup函数中使用toRefs函数来完成此操作 -->
<!-- 如果title是可选的，则传入的props中的title可能没有。
这种情况下toRefs将不会为title创建一个ref，需要使用toRef替代 -->
<!-- 2、context,context是一个普通的javascript对象 
通过context,可以访问到slot attrs emit expose;
data computed methods refs等是访问不到的-->
<!-- 3、结合模版使用， 如果setup中返回一个对象，改对象的property都可以在模版中访问到，
并且在模版中访问时时个浅解析，在模版中使用不需要.value -->
<div>{{titleNew}}</div>
<!-- 4、使用渲染函数 -->
<!-- 5、使用this，setup内部this不是该活跃实例的引用；
因为 setup() 是在解析其它组件选项之前被调用的，所以 setup() 内部的 this 的行为与其它选项中的 this 完全不同。
这使得 setup() 在和其它选项式 API 一起使用时可能会导致混淆。 -->
<!-- 6、生命钩子函数
因为setup是围绕beforeCreate和created生命周期钩子函数运行的，因此不需要显示的定义这两个钩子函数
以下的钩子函数都应该在setup函数中编写 -->
<!-- onBeforeMount -->
<!-- onMounted -->
<!-- onBeforeUpdate -->
<!-- onUpdated -->
<!-- onBeforeUnmount -->
<!-- onUnmounted -->
<!-- onErrorCaptured -->
<!-- onRenderTracked -->
<!-- onRenderTriggered -->
<!-- onActivated -->
<!-- onDeactivated -->
<!-- 7、Provide/Inject -->
<div>{{  userLocation }}</div>
<!-- 8、模版引用 ref-->
<div ref="root">This is a root element</div>
<!-- 9、Mixin,分发vue组件中的复用功能 -->
<!-- // 定义一个 mixin 对象
const myMixin = {
  created() {
    this.hello()
  },
  methods: {
    hello() {
      console.log('hello from mixin!')
    }
  }
}
// 定义一个使用此 mixin 对象的应用
const app = Vue.createApp({
  mixins: [myMixin]
})
 -->
 <!-- 选项合并，发生冲突的时候，以组件的选项为主 -->
 <!-- 钩子函数合并，发生冲突时候，mixin对象钩子在组件自身的钩子函数之前调用 -->
 <!-- 10、自定义指令，需要自己写个demo实践一下 -->
 <!-- 11、插件和编写插件 -->
<slot name="header"></slot>
</template>
<script>
import { toRefs, h, ref, provide, inject, onMounted} from 'vue'
export default {
    props: {
        title: String,
    },
    // watch: {
    //     title(newValue) {
    //         console.log(newValue);
    //     }
    // },
    setup(props, context) {
        // 解构之后props失去响应性
        // const { title } = props;
        // 通过toRefs完成解构操作
        const { title } = toRefs(props)
        // const { title } = toRef(props,'title')
        // Attribute (非响应式对象，等同于 $attrs)
        console.log(context.attrs, 'attrs');
        // 插槽 (非响应式对象，等同于 $slots)
        console.log(context.slots.header, 'slots');
        //  触发事件 (方法，等同于 $emit)
        console.log(context.emit, 'emit')
        // 暴露公共 property (函数
        console.log(context.expose)
        // provide的使用方法
        provide('location', 'North Pole')
        provide('geolocation', {
        longitude: 90,
        latitude: 135
        })
        // inject的使用方法
        const userLocation = inject('user', 'The Universe')
        // const userGeolocation = inject('geolocation')
        // const location = ref('North Pole')
        // 增加provide和inject中的响应性
        // const geolocation = reactive({
        //   longitude: 90,
        //   latitude: 135
        // })

        // provide('location', location)
        // provide('geolocation', geolocation)
        //  更新inject注入的数据，我们可以提供一个更新的方法
        // const updateLocation = () => {
        //     location.value = 'South Pole'
        // }
        // provide('updateLocation', updateLocation)
        // 确保通过provide提供的数据，不会被inject的组件更改，可以用readonly标识为只读
        // provide('updateLocation', readonly(updateLocation))
        // 子组件使用
        //  const updateUserLocation = inject('updateLocation')
        const root = ref(null)
        onMounted(() => {
            // DOM 元素将在初始渲染后分配给 ref
            console.log(root.value) // <div>This is a root element</div>
        })

        return {
            titleNew: title,
            userLocation,
            root,
        }
    },
    // 渲染函数
    // setup(props, { expose }) {
    //     const count = ref(0);
    //     const increment = () => ++count.value
    //     expose({
    //         increment
    //     })
    //     return () => h('div', count.value)
    // }
}
</script>

<style>
</style>

<template>
    <div>
        <!-- 十、基于class的动画和过渡 -->
        <div id="demo">
            Push this button to do something you shouldn't be doing:<br />

            <div :class="{ shake: noActivated }">
                <button @click="noActivated = !noActivated">Click me</button>
                <span v-if="noActivated">Oh no!</span>
            </div>
        </div>
        <!-- 1、性能问题
        transform和opacity,非常好的是，更改 transform 不会触发任何几何形状变化或绘制.这意味着该操作可能是由合成器线程在 GPU 的帮助下执行。
        opacity 属性的行为也类似。因此，他们是在 web 上做元素移动的理想选择。-->
        <!-- 2、硬件加速问题
        诸如：perspective、backface-visibility、transform:translateZ(x)让浏览器知道你需要硬件加速-->
        <!-- 3、 进入过渡和离开过渡效果-->
        <!-- （1）vue会自动嗅探目标元素是否应用了css过渡动画，如果是，在恰当的时机添加/删除 CSS 类名。 -->
        <!-- （2）如果过渡组件提供了 JavaScript 钩子函数 ，这些钩子函数将在恰当的时机被调用。 -->
        <!-- （3）如果没有找到 JavaScript 钩子并且也没有检测到 CSS 过渡/动画，DOM 操作 (插入/删除) 在下一帧中立即执行。 -->
        <!-- 
            （4）钩子函数
            <transition
                @before-enter="beforeEnter"
                @enter="enter"
                @after-enter="afterEnter"
                @enter-cancelled="enterCancelled"
                @before-leave="beforeLeave"
                @leave="leave"
                @after-leave="afterLeave"
                @leave-cancelled="leaveCancelled"
                :css="false"
                >
                </transition>
         -->
        <div id="demo">
             <transition name="fade">
                <p v-if="show">hello</p>
            </transition>
            <button @click="show = !show">Toggle</button>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            noActivated: false,
            show: false,
        }
    }
}
</script>
<style>
.shake {
  animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
  backface-visibility: hidden;
  perspective: 1000px;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
@keyframes shake {
  10%,
  90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%,
  80% {
    transform: translate3d(2px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(4px, 0, 0);
  }
}

</style>

<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <index01 />
  <div>------------------------------------------------------------------</div>
  <index02 />
  <div>------------------------------------------------------------------</div>
  <index03 />
  <div>------------------------------------------------------------------</div>
  <index04 />
  <div>------------------------------------------------------------------</div>
  <index05>
    {{ buttonText }}
     <template v-slot:header>
      <h1>Here might be a page title</h1>
    </template>
  </index05>
  <div>------------------------------------------------------------------</div>
  <index06 />
  <div>------------------------------------------------------------------</div>
  <index07 />
  <div>------------------------------------------------------------------</div>
  <index09 :title='title'/>
</template>
<script>
import index01 from './basicGrammer/index01.vue'
import index02 from './basicGrammer/index02.vue'
import index03 from './basicGrammer/index03.vue'
import index04 from './basicGrammer/index04.vue'
import index05 from './basicGrammer/index05.vue'
import index06 from './basicGrammer/index06.vue'
import index07 from './basicGrammer/index07.vue'
import index09 from './basicGrammer/index09.vue'
export default {
  components: {
    index01,
    index02,
    index03,
    index04,
    index05,
    index06,
    index07,
    index09
  },
  data() {
    return {
      buttonText: 'buttonText1',
      title: 'setup组合api'
    }
  },
  provide: {
    user: 'John Doe hahahah'
  },
  mounted() {
    setTimeout(() => {
      this.title = '更改之后的title'
    }, 100)
  }
}
// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/master/active-rfcs/0040-script-setup.md
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<template>
    <!-- 三、计算属性和侦听器 -->
    <!-- 1、computed计算属性将依赖于他的响应关系进行缓存，计算属性只在相关响应式依赖发生改变时重新求值 -->
    <div>{{ publishedBooksMessage }}</div>
    <!-- 2、watch侦听器:当有些数据需要随着其他数据变化而变化时，可以使用-->
    <div>fullName: {{ fullName }}</div>
    <div>firstName: {{ firstName }}</div>
    <div>lastName: {{ lastName }}</div>
    <div @click="changeFullName">changefullName</div>
    <!-- 3、class和style -->
    <!-- 对象语法 -->
    <div :class="{ active: isActive }">添加样式1</div>
    <div :class="classObject">添加样式2</div>
    <!-- 数组语法 -->
    <div :class="['active', 'bigFont']">添加样式3</div>
    <div :class="['active', hasError ? 'bigFont' : '']">添加样式4</div>
    <div :class="[{ active: isActive }, errorClass]">添加样式5</div>
    <!-- 4、条件语句 -->
    <div v-if="awesome">Vue is awesome!</div>
    <div v-else>else</div>
    <!-- 5、v-show :dom节点是存在的，display为none-->
    <div v-show="awesome">Vue is awesome!</div>
    <!-- 6、v-for的遍历 -->
    <!-- 在v-for中使用数组 -->
    <ul id="array-rendering">
        <li v-for="item in items">
            {{ item }}
        </li>
    </ul>
    <!-- 在v-for中使用对象 -->
    <!-- 在遍历对象的时候，也是按照Object.keys()进行遍历的，
    但是不能保证不同浏览器下的遍历结果是否是一样的 -->
    <ul id="array-rendering">
        <li v-for="(value, name, index) in myObject">
            {{ index }}. {{ name }}: {{ value }}
        </li>
    </ul>
    <!-- 建议尽可能在使用v-for时，提供key的attribute -->
    <!-- 7、数组更新检测 -->
    <!-- 变更方法，变更方法的使用，可以出发视图的更新，因为Vue将被侦听的数组的变更方法进行了包裹 -->
    <!-- push pop sort reverse splice shift unshift  -->
    <!-- 替换数组，当使用数组的非变更方法时，视图不会进行更新（例如：filter, concat, slice）
    它们会生成一个新的数组，导致原来的数据不会变更，因此视图也不会变更；可以用新数组替换旧数组：
     -->
    <!-- 8、监听事件 -->
    <!-- 使用v-on监听事件 -->
    <div id="basic-event">
        <button @click="counter += 1">Add 1</button>
        <p>The button above has been clicked {{ counter }} times.</p>
    </div>
    <div id="event-with-method">
        <!-- `greet` 是在下面定义的方法名 -->
        <button @click="greet($event, 'message', 'hello')">Greet</button>
    </div>
    <!-- 多事件处理器 -->
    <button @click="one($event), two($event)">Submit</button>
    <!-- 事件修饰符 -->
    <!-- stop: 阻止单击事件继续冒泡 -->
    <a @click.stop="doThis">stop</a>

    <!-- prevent: 提交事件不再重载页面 -->
    <form @submit.prevent="onSubmit">prevent</form>

    <!-- 修饰符可以串联 -->
    <a @click.stop.prevent="doThat">.stop.prevent</a>

    <!-- 只有修饰符 -->
    <form @submit.prevent>.prevent</form>

    <!-- 添加事件监听器时使用事件捕获模式 -->
    <!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
    <div @click.capture="doThis">capture</div>

    <!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
    <!-- 即事件不是从内部元素触发的 -->
    <div @click.self="doThat">self</div>
    <!-- 点击事件将只会触发一次 -->
    <a @click.once="doThis">once</a>
    <!-- passive: 表示滚动事件的默认行为，即滚动行为会立即触发，而不会等待onScroll完成； 以防止其中包含 `event.preventDefault()` 的情况  -->
    <!-- 这个 .passive 修饰符尤其能够提升移动端的性能。 -->
    <div @scroll.passive="onScroll">passive</div>
    <!-- 9、按键修饰符 -->
    <!-- 只有在 `key` 是 `Enter` 时调用 `vm.submit()` -->
    <input @keyup.enter="submit" />
    <input @keyup.page-down="onPageDown" />
    <!-- 按键的别名 -->
    <!-- .enter .tab .delete .esc .space .up .down .left .right -->
    <!-- 系统修饰符号 -->
    <!-- .ctrl .alt .shift .meta -->
    <!-- 10、表单绑定输入 -->
    <!-- 基础的语法：首先是v-model指令是在表单input, textarea, select上进行的双向数据绑定；
    v-model只是语法糖，他会根据不同的空控件类型，选取正确的方法来更新值 -->
    <!-- text 和 textarea 元素使用 value property 和 input 事件；
    checkbox 和 radio 使用 checked property 和 change 事件；select 字段将 value 作为 prop 并将 change 作为事件。-->
    <input v-model="message" placeholder="edit me" />
    <p>Message is: {{ message }}</p>

    <span>Multiline message is:</span>
    <p style="white-space: pre-line">{{ message }}</p>
    <br />
    <textarea v-model="message" placeholder="add multiple lines"></textarea>
    <input type="checkbox" id="checkbox" v-model="checked" />
    <div for="checkbox">{{ checked }}</div>
    <!-- 值绑定 -->
    <!-- 对于单选按钮，复选框以及选择框的选项，v-model绑定的值通常是静态字符串或者布尔值 -->
    <!-- 当选中时，`picked` 为字符串 "a" -->
    <input type="radio" v-model="picked" value="a" />
    <!-- 选中时为yes, 没有选中时为no -->
    <input type="checkbox" v-model="toggle" true-value="yes" false-value="no" />
    <select v-model="selected">
        <!-- 内联对象字面量，选中时vm.selected.number // => 123-->
        <option :value="{ number: 123 }">123</option>
    </select>
    <!-- 11、v-model的修饰符号 -->
    <!-- .lazy：每次input事件触发之后，输入框的值和数据进行同步，lazy是在change事件之后进行触发-->
    <input v-model.lazy="msg" @change="inputValueChange('change')" placeholder="等哈哈打电话的话" @input="inputValueChange('input')"/>
    <!-- .number：将用户输入的值自动的转换成数字-->
    <input v-model.number="msg" />
    <!-- .trim：自动过滤用户首位空白字符 -->
    <!-- 12、可以在组件上使用v-model -->
</template>
<script>
export default {
    data() {
        return {
            msg: 'msg',
            checked: false,
            message: 'dkkddkd',
            counter: 0,
            author: {
                name: 'John Doe',
                books: [
                    'Vue 2 - Advanced Guide',
                    'Vue 3 - Basic Guide',
                    'Vue 4 - The Mystery'
                    ]
            },
            firstName: "Doe",
            lastName: "John",
            isActive: true,
            hasError: false,
            awesome: false,
            items: ['han', 'xiao', 'xue'],
            myObject: {
                title: 'How to do lists in Vue',
                author: 'Jane Doe',
                publishedAt: '2016-04-10'
            }
        }
    },
    computed: {
        publishedBooksMessage() {
            console.log('dkdkkddk');
            return this.author.books.length > 0 ? "YES" : "NO"
        },
        // 计算属性的另一种写法，提供了getter和setter方法
        fullName: {
            get() {
                return this.firstName + this.lastName
            },
            set(newValue) {
                const names = newValue.split(' ')
                this.firstName = names[0]
                this.lastName = names[names.length - 1]
            }
        },
        classObject() {
           return {
            active: this.isActive && !this.error,
            'text-danger': this.error && this.error.type === 'fatal'
            } 
        }
    },
    watch: {
        // fullName(newValue, oldValue) {
        //     console.log(newValue, oldValue);
        // },
        fullName: {
            handler(newValue, oldValue) {
                console.log(newValue, oldValue);
            },
            deep: true,
            immediate: true
        }
    },
    methods: {
        changeFullName() {
            this.fullName = 'han xiaoxue'
        },
        greet(event, message, hello) {
            // method内部的this指向的是当前的活动实例
            // event是原生dom中的event
            console.log(event.target.tagName);
            console.log(message, 'message');
            console.log(hello, 'hello');
        },
        one(event) {
            console.log(event, 'one');
        },
        two(event) {
            console.log(event, 'two');
        },
        inputValueChange(value) {
            console.log(value, this.msg, 'input框中的值变化');

        }
    }
}
</script>
<style>
.active {
    color: red
}
.bigFont {
    font-size: 18px;
}
</style>

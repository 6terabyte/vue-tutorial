<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to ようこそ ジャパリパーク" />
    <SampleComponent msg='ぴよ' />
    <SampleComponent />
    {{cnt}}

    <span v-bind:title="message">
      Hover your mouse over me for a few seconds to see my dynamically bound
      title!
    </span>
    <button v-on:click="reverseMessage">Reverse Message</button>
    <p>{{ message }}</p>
    <input v-model="message" />
    <br>
    <span v-if="seen">消える...</span>
    <span v-else>消えた...</span>
    <h1 v-show="seen">Hello!</h1>

    <br>
    <ol>
    <li v-for="todo in todos" :key='todo'>{{ todo.text }}</li>
    </ol> 
    <ol>

      <SampleComponent v-for="item in sampleList"
      v-bind:todo="item"
      v-bind:key="item.id"
      />
    </ol>
    <span>{{  publishedBooksMessage }}</span>
    <div id="watch-example">
  <p>
    Ask a yes/no question:
    <input v-model="question" />
  </p>
  <p>{{ answer }}</p>
  </div>
  <div :class="{ active: isActive }">isactive</div>
  <div
    class="static"
    :class="{ active: isActive, 'text-danger': hasError }">
  </div>
  <div :class="classObject">classObject</div>
  <input @keyup.enter="alert" />

  <div id="demo">
  <button @click="show = !show">
    Toggle render
  </button>

  <transition name="slide-fade">
    <p v-if="show">hello</p>
  </transition>
  </div>

  </div>
</template>

<script src="https://cdn.jsdelivr.net/npm/axios@0.12.0/dist/axios.min.js"></script>
<script>
import HelloWorld from './components/HelloWorld.vue'
import SampleComponent from './components/SampleComponent.vue'
export default {
  name: 'App',
  data:()=>({
    cnt: 1,
    message: 'You loaded this page on ' + new Date().toLocaleString(),
    seen : true,
    todos: [
        { text: '内科' },
        { text: '麻酔科' },
        { text: '精神科' },
        {text : '心療内科'}
      ],
      sampleList:[
        {id:0,text:"text1"},
        {id:0,text:"text2"},
        {id:0,text:"text3"},
        {id:0,text:"text4"},
      ],
    question: '',
    answer: 'Questions usually contain a question mark. ;-)',
      isActive: true,
      hasError: false,
      error: null,
      show: true,
    }),
      watch: {
      question(newQuestion, oldQuestion) {
        if (newQuestion.indexOf('?') > -1) {
          this.getAnswer()
        }
      }
    },
    computed: {
    publishedBooksMessage() {
      return this.todos.length
    },
    classObject() {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
  },
  components: {
    HelloWorld,
    SampleComponent
  },
  methods:{
    reverseMessage(){
      this.message = this.message
      .split('')
      .reverse()
      .join('');
      this.seen = !this.seen;
    }, 
    getAnswer() {
        this.answer = 'Thinking...'
        /*
        axios
          .get('https://yesno.wtf/api')
          .then(response => {
            this.answer = response.data.answer
          })
          .catch(error => {
            this.answer = 'Error! Could not reach the API. ' + error
          })
          */
        setTimeout(()=>{
        this.answer = 'answer ' 

        },1000)
    },
    alert(){
      window.alert('alert')
    }
  },
  mounted() {
    setInterval(() => {
      this.cnt++
    }, 1000)
  }
}
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
.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
</style>

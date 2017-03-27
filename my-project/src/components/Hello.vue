<template>
  <div class="hello">
    <h1>{{ msg| filterA | filterB }}</h1>
    <h2>{{inputValue}}</h2>
    <span v-bind:title="message">
        Hover your mouse over me for a few seconds to see my dynamically bound title!
    </span>
    <p v-if="seen">Now you see me</p>
    <ol>
        <li v-for="todo in todos">
            {{ todo.text }}
        </li>
    </ol>
    <ul>
        <li><button v-on:click="reverseMessage">Reverse Message</button></li>
        <li><span>{{tips}}</span></li>
        <li><input v-model="inputValue" :class="{'text-danger':hasError}"></li>
    </ul> 
    
  <my-button :title="buttonTitle"></my-button>
  <div :style="styleObject">{{reversedMessage}}</div>
  <div>{{reverseMessages()}}</div>
    <h1 v-if="ok">Yes</h1>
    <h1 v-else>No</h1>
    <ul>
        <template v-for="(value,key) of items">
            <li>{{ key }} : {{ value }}</li>
            <li class="divider"></li>
        </template>
</ul>
<TodoList></TodoList>
<li v-for="n in evenNumbers" :key="n">{{ n }}</li>
<button v-on:click="warn('Form cannot be submitted yet.', $event)">Submit</button>
<br/>
<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>
<br>
<input type="checkbox" v-model="toggle" v-bind:true-value="a" v-bind:false-value="b">
<label for="checkbox">{{ toggle }}</label>
<br/>
<input type="radio" id="one" v-model="pick" v-bind:value="a">
<label for="one">{{a}}</label>
<br>
<input type="radio" id="two" v-model="pick" v-bind:value="b">
<label for="two">{{b}}</label>
<br/>
<span>Picked: {{ pick }}</span>
<br>
<select v-model="selected">
  <option v-for="option in options" v-bind:value="option.value">
    {{ option.text }}
  </option>
</select>
<span>Selected: {{ selected }}</span>
<br>
<span>Count:{{count}}</span>
</div>
</template>
<script>
    import MyButton from 'components/Button'
    import TodoList from 'components/TodoList'
    import Vuex from 'vuex'
    export default {
        name: 'hello',
        data() {
            return {
                selected: 'A',
                options: [{
                    text: 'One',
                    value: 'A'
                }, {
                    text: 'Two',
                    value: 'B'
                }, {
                    text: 'Three',
                    value: 'C'
                }],
                toggle: "Two",
                pick: "",
                a: "One",
                b: "Two",
                checked: false,
                numbers: [1, 2, 3, 4, 5],
                inputValue: '',
                tips: '',
                ok: false,
                items: {
                    FirstName: 'John',
                    LastName: 'Doe',
                    Age: 30
                },
                hasError: false,
                msg: 'welcome to vue app!',
                buttonTitle: "I'm Button",
                message: 'You loaded this page on ' + new Date(),
                seen: true,
                todos: [{
                    text: 'Learn JavaScript'
                }, {
                    text: 'Learn Vue'
                }, {
                    text: 'Build something awesome'
                }],
                styleObject: {
                    color: 'red',
                    fontSize: '13px'
                }
            }
        },
        computed: {
            // a computed getter
            reversedMessage() {
                // `this` points to the vm instance
                return this.msg + Date.now()
            },
            evenNumbers() {
                return this.numbers.filter(function(number) {
                    return number % 2 === 0
                })
            },
            count() {
                return this.$store
            }
        },
        watch: {
            // 如果 inputValue 发生改变，这个函数就会运行
            inputValue() {
                if (this.inputValue != '123') {
                    this.hasError = true
                    this.tips = 'please input 123'
                } else {
                    this.hasError = false
                    this.tips = 'correct input'
                }
            }
        },
        filters: {
            filterA(value) {
                if (!value) return ''
                value = value.toString()
                var reg = /\b(\w)|\s(\w)/g;
                return value.replace(reg, function(m) {
                    return m.toUpperCase()
                })
            },
            filterB(value) {
                if (!value) return ''
                value = value.toString()
                return value.replace(/\s/g, "@")
            }
        },
        methods: {
            reverseMessage() {
                this.inputValue = this.inputValue.split(' ').reverse().join(' ')
            },
            reverseMessages() {
                return this.msg + Date.now()
            },
            warn(message, event) {
                // 现在我们可以访问原生事件对象
                if (event) event.preventDefault()
                alert(message)
            }
        },
        components: {
            MyButton,
            TodoList,
            Vuex
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h1,
    h2 {
        font-weight: normal;
    }
    
    ul {
        list-style-type: none;
        padding: 0;
    }
    
    a {
        color: #ff8c00;
    }
    
    .text-danger {
        background: red;
    }
</style>
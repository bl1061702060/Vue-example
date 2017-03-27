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
  <div>{{reverseMessage()}}</div>
    <h1 v-if="ok">Yes</h1>
    <h1 v-else>No</h1>
    <ul>
        <template v-for="(value,key) of items">
            <li>{{ key }} : {{ value }}</li>
            <li class="divider"></li>
        </template>
</ul>
<TodoList></TodoList>
</div>
</template>
<script>
    import MyButton from 'components/Button'
    import TodoList from 'components/TodoList'
    export default {
        name: 'hello',
        data() {
            return {
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
            reversedMessage: function() {
                // `this` points to the vm instance
                return this.msg + Date.now()
            }
        },
        watch: {
            // 如果 inputValue 发生改变，这个函数就会运行
            inputValue: function() {
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
            filterA: function(value) {
                if (!value) return ''
                value = value.toString()
                var reg = /\b(\w)|\s(\w)/g;
                return value.replace(reg, function(m) {
                    return m.toUpperCase()
                })
            },
            filterB: function(value) {
                if (!value) return ''
                value = value.toString()
                return value.replace(/\s/g, "@")
            }
        },
        methods: {
            reverseMessage: function() {
                return this.msg + Date.now()
            }
        },
        components: {
            MyButton,
            TodoList
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
        color: #42b983;
    }
    
    .text-danger {
        background: red;
    }
</style>
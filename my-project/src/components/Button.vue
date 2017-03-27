<template>
    <div class="my-button">
        <div class="button" v-on:click="buttonClick" >{{title}}</div>
    </div>
</template>
<script>
    import Vue from 'vue'
    export default {
        name: 'Button',
        props: {
            'title': {
                type: String,
                required: true
            }
        },
        methods: {
            buttonClick: function() {
                alert(this.title);
            }
        },
        components: {
            Vue
        }
    }
</script>
<style scoped>
    .my-button {
        text-align: center;
    }
    
    .button {
        display: inline-block;
        border-radius: 7px;
        padding: 3px 7px;
        box-shadow: 3px 3px 10px grey;
        background: -webkit-linear-gradient(#fff, #e1e1e2);
        /* Safari 5.1 - 6.0 */
        background: -o-linear-gradient(#fff, #e1e1e2);
        /* Opera 11.1 - 12.0 */
        background: -moz-linear-gradient(#fff, #e1e1e2);
        /* Firefox 3.6 - 15 */
        background: linear-gradient(#fff, #e1e1e2);
        /* 标准的语法 */
    }
    
    .button:active {
        display: inline-block;
        border-radius: 7px;
        padding: 3px 7px;
        color: #fff;
        box-shadow: 3px 3px 10px #547def;
        background: -webkit-linear-gradient(#63b5f7, #547def);
        /* Safari 5.1 - 6.0 */
        background: -o-linear-gradient(#63b5f7, #547def);
        /* Opera 11.1 - 12.0 */
        background: -moz-linear-gradient(#63b5f7, #547def);
        /* Firefox 3.6 - 15 */
        background: linear-gradient(#63b5f7, #547def);
        /* 标准的语法 */
    }
</style>
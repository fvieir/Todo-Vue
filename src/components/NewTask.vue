<template>
    <div class="new-task">
        <input @keyup.enter="add" v-model="name" type="text"
            class="form-element" placeholder="Nova Tarefa ?">
        <button class="form-element" @click="add">+</button>
    </div>
</template>

<script>
    export default {
        data () {
            return{
                name: ''
            }
        },
        methods:{
            add () {
                this.$emit('taskAdded', {name: this.name})
                this.name = ''
            }
        }
    }
</script>

<style lang="scss" scoped>
    .new-task{
       margin: 35px; 
    }
    .form-element{
        outline: none;
        padding: 5px 10px 5px 10px;
        font-size: 1.2rem;
        border: 1px solid #fff;
    }
    input.form-element{
        width: 500px;
        border-top-left-radius: 8px;
        border-bottom-left-radius: 8px;
        background-color: #fFF2;
        color: #ccc;
    }
    button.form-element{
        background-color:#2196f3;
        border-top-right-radius: 8px;
        border-bottom-right-radius: 8px;
    }
</style>
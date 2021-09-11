<template>
    <div 
        @click="$emit('taskStateChanged',task)" 
        class="task" 
        :class="stateClass">
        <span class="close" 
              @click.stop="$emit('deleteTask', task)">x</span>
        <p>{{task.name}}</p>
    </div>
</template>

<script>
    export default {
        props:{
            task:{
                type: Array,
                required: true
            }
        }, 
        methods:{
           
        },
        computed: {
            stateClass() {
                return {
                    pending: this.task.pending,
                    done: !this.task.pending
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    .task{
        position: relative;
        box-sizing: border-box;
        width: 200px;
        height: 150px;
        padding: 10px;
        font-size: 1.4rem;
        font-weight: 300;
        cursor: pointer;
        user-select: none;
        display: flex;
        justify-content: center;
        align-items: center;
        word-break: break-all;
    }
    .pending{
        border-left: 12px solid rgba(255, 0, 0, 0.281);
        background-color: rgba(197, 7, 7, 0.747);
    }
    .done{
        border-left: 12px solid rgba(0, 128, 0, 0.301);
        background-color:#4CAF50;
        text-decoration: line-through;
    }
    .close{
        font-size: 0.9rem;
        font-weight: 600;
        position: absolute;
        top: 10px;
        right: 10px;
        width: 20px;
        height: 25px;
        border-radius: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .pending .close{
        background-color: #b73229;
    }
    .pending .done{
        background-color: #4caf4c;
    }
</style>
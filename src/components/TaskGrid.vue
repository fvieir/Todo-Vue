<template>
    <div class="taks-grid">
       <template v-if="tasks.length">
            <task v-for="task in tasks" :key="task.name" 
                @taskStateChanged="$emit('taskStateChanged', $event)"
                @deleteTask="$emit('deleteTask', $event)" 
                :task="task"/>
       </template>
       <p v-else class="no-task">Sua Vida esta em dia !</p>
    </div>
</template>
<script>
    import Task from './Task.vue'
    export default {
        props:{
            tasks: {type: Array, required: true}
        },
        components:{Task},
    }
</script>

<style lang="scss" scoped>
    .taks-grid{
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    }
    .taks-grid .task {
        margin: 10px;
    }
    .no-task{
        color: #fff;
        font-size: 1.5rem;
    }

</style>
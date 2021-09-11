<template>
  <div id="app">
    <h1>Tarefas</h1>
    <TaskProgressBar
      :progress="progress"/>

    <NewTask 
      @taskAdded="addTask"/>

    <TaskGrid 
      :tasks="tasks" 
      @taskStateChanged="toggleTaskState"
      @deleteTask="taskDelete"/>
   
  </div>
</template>

<script>
  import TaskGrid from './components/TaskGrid.vue'
  import NewTask from './components/NewTask.vue'
  import TaskProgressBar from './components/TaskProgressBar.vue'

  export default {
      components:{TaskGrid, NewTask, TaskProgressBar},
      data () {
          return {
              tasks: []
          }
      },
      methods: {
          addTask (task) {
              const sameName =  this.tasks.filter(t => t.name === task.name) // Verifica se existe um nome que ja esta no tasks
              const reallNew = sameName.length === 0 // Se o tamanho do resultado do array for igual a 0 retorna true
            
              if(reallNew){
                  if(task.name === '') return false 
                  
                  this.tasks.push({
                      name: task.name,
                      pending: this.pending || true
                  })
              }
          },
          taskDelete (taks) {
              let i = this.tasks.indexOf(taks) // Procura dentro do array o indice do objeto
              if(i >= 0) this.tasks.splice(i,1) // Se o indice maior que 0 exlcuir o elemento com função splice
          },
          toggleTaskState(task){
            const update = this.tasks.filter(t => t.name === task.name)
            update[0].pending = !update[0].pending
          }
      },
      computed:{
        progress(){
          const resul = this.tasks.filter(t => !t.pending).length
          const total = this.tasks.length
          return Math.round(Number(resul) / Number(total) * 100) || 0
        }
      },
      watch:{
        tasks: {
          deep:true,
          handler(){
            localStorage.setItem('tasks', JSON.stringify(this.tasks))
          }
        }
      },
      created(){
        const json = localStorage.getItem('tasks')
        const array = JSON.parse(json) 
        this.tasks = Array.isArray(array) ? array : []
      }
  }
</script>

<style lang="scss">
body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}
#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>

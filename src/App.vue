<template>
<div class="container">
  <Header :showAddTask="showAddTask" @toggle-add-task="toggleAddTask" />
  <AddTask v-show="showAddTask" @add-new-task="addTaskToData" />
  <Tasks @toggle-remainder="toggleRemainder" @delete-task="deleteTask" :tasks="tasks" />
  <Footer />
</div>
  

  
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Header,
    Footer,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  methods: {
    async deleteTask(id){
      if (confirm('Are you sure?')){
        const res = await fetch(`http://localhost:5001/tasks/${id}`
        , {
          method: 'DELETE',
        })
      console.log(res)
        res.status === 200 ? 
        (this.tasks = this.tasks.filter(each => each.id !== id)):
        alert('Error deleting task')
      }
    },
    async toggleRemainder(id){
      const taskToToggle = await this.fetchTask(id)

      const updatedTask = {...taskToToggle, remainder: !taskToToggle}

      const res = await fetch(`http://localhost:5001/tasks/${id}`
      , {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updatedTask)
      })

      const data = await res.json()

      this.tasks = this.tasks.map( each => each.id === id ? {...each, remainder: data.remainder}:{...each})
      // console.log(id)
    },
    async addTaskToData(task){
      const res = await fetch('http://localhost:5001/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      })

      const data = await res.json()

      this.tasks = [...this.tasks, data]
    },
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
    async fetchTasks() {
      const response = await fetch('http://localhost:5001/tasks')

      const data = await response.json()
      return data
    },
    async fetchTask(id) {
      const response = await fetch(`http://localhost:5001/tasks/${id}`)

      const data = await response.json()
      return data
    }
  },
  async created(){
    this.tasks = await this.fetchTasks()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}

.container{
  border: 3px solid #7fb7f0;
  border-radius: 4px;
  padding: 12px;

}
</style>

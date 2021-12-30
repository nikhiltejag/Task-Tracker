<template>
    <AddTask v-show="showAddTask" @add-new-task="addTaskToData" />
  <Tasks @toggle-remainder="toggleRemainder" @delete-task="deleteTask" :tasks="tasks" />
</template>

<script>
import Tasks from '../components/Tasks.vue'
import AddTask from '../components/AddTask.vue'

export default {
    name: 'Home',
    props: {
        showAddTask: Boolean,
    },
    components: {
        Tasks,
        AddTask
    },
    data(){
        return {
            tasks: [],
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
  // console.log('before',taskToToggle)
      const updatedTask = {...taskToToggle, remainder: !taskToToggle.remainder}
      // console.log('updated',updatedTask)
      const res = await fetch(`http://localhost:5001/tasks/${id}`
      , {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updatedTask)
      })

      const data = await res.json()
      // console.log('updated to db',data)
      this.tasks = this.tasks.map( each => each.id === id ? {...each, remainder: data.remainder}:{...each})
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
<template>
<div class="container">
  <Header :showAddTask="showAddTask" @toggle-add-task="toggleAddTask" />
  <AddTask v-show="showAddTask" @add-new-task="addTaskToData" />
  <Tasks @toggle-remainder="toggleRemainder" @delete-task="deleteTask" :tasks="tasks" />
</div>
  

  
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Header,
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
    deleteTask(id){
      if (confirm('Are you sure?')){
        this.tasks = this.tasks.filter(each => each.id !== id)
      }
    },
    toggleRemainder(id){
      this.tasks = this.tasks.map( each => each.id === id ? {...each, remainder: !each.remainder}:{...each})
      // console.log(id)
    },
    addTaskToData(task){
      this.tasks = [...this.tasks, task]
    },
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    }
  },
  created(){
    this.tasks = [
      {
        id:1,
        text: 'Doctors Appointment',
        day: 'March 1st at 2:30pm',
        remainder: true,
      },
      {
        id:2,
        text: 'Doctors Farewell',
        day: 'March 1st at 4:30pm',
        remainder: false,
      },
      {
        id:3,
        text: 'Movie Time',
        day: 'March 2nd at 2:30pm',
        remainder: true,
      }
    ]
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

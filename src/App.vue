<template>
<div class="container">
  <Header :showAddTask="showAddTask" @toggle-add-task="toggleAddTask" />
  <router-view :showAddTask="showAddTask"></router-view>
  <Footer />
</div>
  

  
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Footer,
  },
  data() {
    return {
      showAddTask: false,
    }
  },
  methods: {
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
  
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

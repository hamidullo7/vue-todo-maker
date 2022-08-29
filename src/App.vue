<template>
<div class="container">
 <Header :showAddTasks="showAddTasks" @toggle-add-task="toggleAddTask" title="Task tracker" />
 <div v-show="showAddTasks">
 <AddTask @add-task="addTask" />

 </div>
 <Tasks
  @toggle-reminder="toggleReminder"
  @delete-task="deleteTask" :tasks="tasks" />
</div>

</template>

<script>
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'
export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data(){
    return{
      tasks: [],
      showAddTasks: false
    }
  },
  methods:{
    deleteTask(id){
      if(confirm("Are you sure? "))
      this.tasks = this.tasks.filter(task => task.id !== id)
    },
    toggleReminder(id){
      // console.log('a')
      this.tasks = this.tasks.map(task => {
        if (task.id === id) task.reminder = !task.reminder
        return task
      })
    },
    addTask(task){
      this.tasks = [...this.tasks, task]
    },
    toggleAddTask(){
      this.showAddTasks = !this.showAddTasks
    }
  },
  created(){
    this.tasks = [
      {
        id: 1,
        text: "tx3",
        day: 'march 1',
        reminder: true
      },{
        id: 2,
        text: "tx3",
        day: 'march 1',
        reminder: true
      },{
        id: 3,
        text: "tx3",
        day: 'march 1',
        reminder: false
      },{
        id: 4,
        text: "tx3",
        day: 'march 1',
        reminder: true
      },{
        id: 5,
        text: "tx3",
        day: 'march 1',
        reminder: true
      },
    ]
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
</style>

<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" :showAddTaskButton="showAddTask" title="Tasks Tracker"/>
    <div v-if="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" /> 
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'

export default {
  name: 'App',
  components: {
    //HelloWorld
    Header,
    Tasks,
    AddTask
  },
  methods:{
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
    addTask(task){
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id)
    {
      if(confirm('Are you sure?'))
      {
        this.tasks = this.tasks.filter((task)=> task.id !== id)
      }
    },
    toggleReminder(id)
    {
      this.tasks = this.tasks.map((task)=>{
        return task.id === id ? {...task, reminder: !task.reminder} : task
      })
    },
  },
  data(){
    return{
      tasks: [],
      showAddTask: false
    }
  },
  created(){
    this.tasks = [
      {
        id: 1,
        text: "Playing basketball",
        day: "March 1st at 2:45pm",
        reminder: true
      },
      {
        id: 2,
        text: "Riding a big bike",
        day: "March 2nd at 3:45am",
        reminder: true
      },
      {
        id: 3,
        text: "Watching a movie",
        day: "March 3rd at 10:00am",
        reminder: false
      }
    ]
  }
}
</script>

<style>
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
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>

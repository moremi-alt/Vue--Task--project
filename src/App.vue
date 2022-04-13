<template>
<div class="container">
 <Header @toggle-add-task="toggleAddTask" title="fast tracker"
 :showAddTask="showAddTask"/>
 <div v-show="showAddTask">
 <AddTask @add-task="addTask" />
 </div>
  <Tasks 
  @toggle-reminder="toggleReminder" 
  @delete-task="deleteTask" 
  :tasks="tasks"
  />
  <Footer />
</div>
</template>

<script>

import Header from './components/Header'
import Tasks  from  './components/Tasks'
import  AddTask from './components/AddTask'
import Footer from './components/Footer'

export default {
  name: 'App',
  components:{
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
    toggleAddTask() {
           this.showAddTask = !this.showAddTask
    },
    addTask(task){
              this.tasks=[...this.tasks,task]
    },
    deleteTask(id) {
      if (confirm('Are you sure?')) {
      this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    toggleReminder(id){
               this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder} : task)
    },
  },
  created() {
    this.tasks = [
      {
        id:1,
        text:'Doctors visitation',
        day:'23rd March at 1:23pm',
        reminder:true,
      },
      {
        id:2,
        text:'Meeting at School',
        day:'June 23rd at 12:00pm',
        reminder:true,
      },
    {
      id:3,
      text:'Food Shopping',
      day:'Narch 3rd at 11:00am',
      reminder:false,
   }
    ]
  },

}  
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
* { 
  box-sizing: border-box;
  margin: 0;
  padding: 0;

}
body{
    font-family: 'poppins',sans-serif;
}
.container{
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn{
  display: inline-block;
  background: #000;
  color:#fff;
  border:none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor:pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline:none;
}
.btn:active {
   transform: scale(0.98);
}
.btn:block {
   display: block;
   width: 100%;
}
</style>

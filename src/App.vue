<template>
 <div class="container">
  <HeaderItem @toggle-add-task='toggleAddTask' title='Task Tracker' :showAddTask='showAddTask' />
  <div v-show='showAddTask'>
    <AddTask @add-task="addTask" />
  </div>

  <TasksItems @toggle-reminder="toggleReminder" @delete-task="deleteTask"  :tasks="tasks" />
 </div>

</template>

<script>
import HeaderItem from './components/Header.vue'
import TasksItems from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    HeaderItem,
    TasksItems,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: {
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },

    addTask(task) {
      this.tasks = [...this.tasks, task]
    },

    deleteTask(id) {
      if(confirm('Are you sure?')){
         this.tasks = this.tasks.filter((task) => task.id !== id )
      }
    },
    toggleReminder(id){
      console.log(id)
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder} : task)
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Take a bath',
        day: 'April 1st at 8am',
        reminder: true
      },
      {
        id: 2,
        text: 'Go to Work',
        day: 'April 1st at 9am',
        reminder: false
      },
      {
        id: 3,
        text: 'Walk the dog',
        day: 'April 1st at 9pm',
        reminder: true
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
  padding: 0
}

body {
  font-family: 'Poppins', sans-serif
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
  background: rgb(27, 167, 34);
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
</style>

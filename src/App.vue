<template>
  <div class="container">
    <Header
      v-on:toggle-add-task="handleToggleForm"
      v-bind:showAddButton="showAddTask"
      title="Hola, soy un prop"
      />
    <div>
      <AddTask
        v-if="showAddTask" 
        v-on:new-task-emit="handleNewTask" 
        />
    </div>
    <Tasks
      v-on:toggle-reminder="handleToggle"
      v-on:delete-task="handleDelete"
      v-bind:tasks="tasks"
    />
  </div>
</template>

<script>
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask"
export default {
  name: "App",
  components: {
    AddTask,
    Header,
    Tasks,
  },
  methods: {
    handleDelete(id) {
      if (confirm("Seguro?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    handleToggle(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
    handleNewTask(newTask){
       this.tasks = [newTask, ...this.tasks];
    },
    handleToggleForm(){
      this.showAddTask = !this.showAddTask
    },
    async fetchTasks(){
      const res = await fetch('http://localhost:5000/tasks');
      const data = await res.json();
      return data
    }
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    };
  },
  async created() {
   this.tasks = await this.fetchTasks()
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
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

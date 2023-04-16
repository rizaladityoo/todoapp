<template>
  <div class="container py-5">
    <h1 class="display-4 mb-4">My To-Do List</h1>
      <div class="mb-4">
        <div class="input-group">
          <input
            type="text"
            class="form-control"
            placeholder="Add a new task"
            name="task"
            v-model="task"
          />
          <button type="submit" class="btn btn-success" @click="addTask">Add Task</button>
        </div>
      </div>
      
      <ul class="list-group">
        <li v-for="(task, index) in tasks" :key="index" class="list-group-item d-flex justify-content-between align-items-center" @click="changeStatus(index)">
          <span :class="{'text-decoration-line-through':task.status=='Completed'}">{{ task.name }}</span>
          <div>
            <span :class="{
              'text-warning':task.status=='Started',
              'text-success':task.status=='Completed'
              }">{{ task.status }}</span>
            <button class="btn btn-primary me-2" @click="showModal = true">Edit</button>
            <button class="btn btn-danger" @click="deleteTask(index)">Delete</button>
          </div>
        </li>
        <!-- Add more tasks here -->
      </ul>
  </div>
  
  
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      tasks : [
        {
          name: 'Do homework',
          status: 'Started'
        },
        {
          name: 'Fasting',
          status: 'Completed'
        },
      ],
      task:""
    }
  },
  methods:{
    changeStatus(index){
      if (this.tasks[index].status === 'Started') {
        this.tasks[index].status = 'Completed'
      } else if (this.tasks[index].status === 'Completed') {
        this.tasks[index].status = 'Started'
      }
    },
    addTask(){
      if(this.task){
        this.tasks.push({
          name: this.task,
          status: 'Started'
        })}
    },
    deleteTask(index){
      this.tasks.splice(index,1)
    }
  },
  mounted(){
    this.changeStatus()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->


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
        <li v-for="(task, index) in tasks" :key="index" class="list-group-item d-flex justify-content-between align-items-center">
          <span :class="{'text-decoration-line-through':task.status=='Completed'}"  @click="changeStatus(index)">{{ task.name }}</span>
          <div>
            <span :class="{
              'text-warning':task.status=='Started',
              'text-success':task.status=='Completed'
              }">{{ task.status }}</span>
            <button class="btn btn-primary me-2" @click="showModal(index)">Edit</button>
            <button class="btn btn-danger" @click="deleteTask(index)">Delete</button>
          </div>
        </li>
        <!-- Add more tasks here -->
      </ul>
  </div>
  <div class="modal fade" ref="myModal">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">Edit Task</h5>
            <button type="button" class="btn-close" @click="hideModal"></button>
          </div>
          <div class="modal-body">
            <input
              type="text"
              class="form-control"
              v-model="edit_modal"
            />
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" @click="hideModal">Close</button>
            <button type="button" class="btn btn-primary" @click="editModal">Save changes</button>
          </div>
        </div>
      </div>
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
      task:"",
      edit_modal:"",
      index_edit_model:null,
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
    },
    showModal(index) {
      this.$refs.myModal.classList.add("show");
      this.$refs.myModal.style.display = "block";
      this.edit_modal = this.tasks[index].name
      this.index_edit_model = index
    },
    hideModal() {
      this.$refs.myModal.classList.remove("show");
      this.$refs.myModal.style.display = "none";
    },
    editModal() {
      this.tasks[this.index_edit_model].name = this.edit_modal
      this.edit_modal = ""
      this.index_edit_model = null
      this.$refs.myModal.classList.remove("show");
      this.$refs.myModal.style.display = "none";
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->


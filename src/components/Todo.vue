<template>
  <h1>ToDoApp</h1>

  <div class="todo">
    <div class="todo-container">
      <div class="input-group mb-3">
        <input
          type="text"
          class="form-control"
          placeholder="Type a task name"
          v-model="inputTask"
        >
        <button
          class="btn btn-outline-secondary"
          type="button"
          id="button-addon2"
          @click="addTask"
        >Add</button>
      </div>
      <ul class="list-group"  >
        <li v-for="task in taskList" class="list-group-item list-group-item-action" v-bind:key="task.name" >
          <div class="form-check">
            <input class="form-check-input" type="checkbox" @click="task.finished = !task.finished" id="listCheck">
            <label class="form-check-label" for="listCheck" v-bind:class="task.finished ? '--finished-task' : '' ">
              {{task.name}}
            </label>
            <ion-icon class="float-end" name="trash-bin-outline" @click="() => removeTask(task)"></ion-icon>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Todo",
    data() {
      return {
        inputTask: '',
        taskList: [{"name": "Text", finished: false}]
      }
    },
    methods: {
      addTask() {
        this.taskList.push({name: this.inputTask, finished: false})
      },
      removeTask(task) {
        this.taskList = this.taskList.filter(taskInList => task!=taskInList)
      }
    }
    
  }
</script>

<style scoped>
  .todo {
    max-width: 500px;
    margin: 0 auto;
  }

  .todo-container {
    display: flex;
    flex-direction: column;
  }

  .form-check-label{
    word-break: break-all;
  }

  .--finished-task{
    text-decoration: line-through;
  }

  ion-icon:hover{
    cursor: pointer;
  }
</style>
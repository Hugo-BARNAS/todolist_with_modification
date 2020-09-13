<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <form v-on:submit.prevent="addTask()">
      <input type="text" placeholder="Tâche à faire" v-model="task" />
      <button type="submit">Ajouter</button>
    </form>
    <ul>
      <li
      v-bind:class="{completed:task.done}"
      v-on:click="task.done = !task.done"
        v-for="task in taskData"
        :key="task.taskData"
      >
      <span v-if="!task.isInEditMode">
        <i class="fa fa-edit" v-on:click="switchMode(task)"></i>
        {{ task.description }}
        <i class="fa fa-trash" v-on:click="deleteTask(task)"></i>
      </span>
      <span v-else>
        <i class="fa fa-thumbs-o-up"></i>
        <input type="text" v-model="task.description" v-on:keyup.enter="switchMode(task)">
      </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "todolist",
  props: {
    msg: String,
  },
  data() {
    return {
      task: null,
      taskData: [],
    };
  },
  methods: {
    addTask: function() {
      this.taskData.push({
        id: Date.now(),
        description: this.task,
        done: false,
        isInEditMode:false
      });
      console.log("taskData", this.taskData);
      this.task = null;
    },
    switchMode:function(task){
      task.isInEditMode=!task.isInEditMode;
    },
    deleteTask:function(task){
      this.taskData = this.taskData.filter(function(t){
       return t.id !== task.id}) 
    },
  },
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>

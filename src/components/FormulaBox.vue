<template>
  <div class="formula-box" :id="formId">
    <FormulaHeader
      :boxMonth="boxMonth"
      :day="day"
      :year="year"
    />
    <component :tasks="tasks" :formId="formId" :is="activeTab" @refreshTasks="refreshTasks($event)" @colorBox="colorBox($event)" @taskToDelete="taskToDelete($event)"/>
    <div class="select-components">
      <button class="list-btn" @click="activeTab='Tasks'"> List</button>
      <button class="formula-btn" @click="activeTab='AddTask'">Add</button>
    </div>
  </div>
</template>

<script>
import Tasks from './Tasks.vue'
import FormulaHeader from './FormulaHeader.vue'
import AddTask from './AddTask.vue'
export default {
components:{
  Tasks,
  FormulaHeader,
  AddTask,
},
props:{
   year: Number,
   boxMonth: String,
   day: Number,
   formId: String,
   tasks: Array
},
data(){
  return{
    activeTab: 'Tasks',
  }
},
methods:{
  newTask(n){
    this.$emit('newTask',n);
  },
  refreshTasks(n){
    this.$emit('refreshTasks', n);
  },
  colorBox(n){
    this.$emit('colorBox', n);
  },
  taskToDelete(n){
    this.$emit('taskToDelete', n);
  }
},
updated(){
}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
.select-components{
width: 100%;
height: 80px;
display: flex;
justify-content: space-around;
align-items: center;
}
.list-btn, .formula-btn{
  height: 100%;
  width: 70px;
  border-radius: 50px;
  font-size: 18px;
  color: white;
  background: transparent;
  border: none;
  cursor: pointer;
}

.formula-box{
    height: 600px;
    width: 400px;
    background: #595B83;
    border-radius: 50px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
    box-shadow: 0px 5px 10px #060930;
}

h3{
  font-size: 28px;
}

@media only screen and (max-width: 1255px){
    .formula-box{
        width: 350px;
    }
}
@media only screen and (max-width: 1100px){
  .formula-box{
    width: 300px;
    height: 500px;
  }
}
@media only screen and (max-width: 940px){
  .formula-box{
    height: 30vh;
    width: 100%;
    border-radius: 0px;
  }
  .select-components{
    height: 50px;
  }
}
</style>
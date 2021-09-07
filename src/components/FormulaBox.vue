<template>
  <div class="formula-box">
    <FormulaHeader />
    <Tasks />
    <AddTask />
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
data(){
  return{
    test: false,
  }
}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
.formula-box{
    height: 600px;
    width: 400px;
    background: #595B83;
    border-radius: 50px;
    display: flex;
    justify-content: center;
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
}
</style>
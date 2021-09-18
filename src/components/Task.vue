<template>
<transition name="drop">
  <div class="task">
      <div class="task-content" @click="openInfo()" :class="{close:isDeleted}"> <p class="time">{{task.time}}</p> <p class="title">{{task.title}}</p> </div>
      <button class="delete-btn" @click="deleteTask()" :class="{close:isDeleted}"><img class="delete-img" src="../assets/trash.svg" alt="thrash"></button>
  </div>
</transition>
</template>

<script>
export default {
props:{
    task: Object,
},
data(){
    return{
        isOpened: false,
        isDeleted: true,
    }
},
methods:{
    deleteTask(){
        this.isDeleted=true;
        this.$emit('taskToDelete', this.task);
    },

    openInfo(){
        this.$emit('isOpened', this.isOpened);
        this.$emit('taskInfo', this.task);
    }
}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
.close{
  animation: wobble 0.2s ease !important;
}
@keyframes wobble{
  0%{
    transform: translateX(-4px);
  }
  20%{
    transform: translateX(4px);
  }
  80%{
    transform: translateX(-4px);
  }
  100%{
    transform: translateX(4px);
  }
}
.task{
    width: 100%;
    height: 50px;
    display: flex;
    justify-content: space-around;
    align-items: center;
}
.task-content{
    width: 250px;
    height: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    border-radius: 50px;
    cursor: pointer;
    background-color: white;
}
.task-content:hover{
    background-color: #f5f7fa;
}
.time{
    width: 40%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Montserrat', sans-serif;
    font-size: 22px;
    font-weight: 400;
    font-weight: bold;
}
.title{
    width: 60%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Montserrat', sans-serif;
    font-size: 16px;
}
.delete-btn{
    height: 50px;
    width: 50px;
    border-radius: 50%;
    background: #f76d6d;
    border:none;
    cursor: pointer;
}
.delete-img{
    height: 30px;
    width: 35px;
}
@media only screen and (max-width: 1100px){
    .time{
        font-size: 16px;
    }
    .title{
        font-size: 14px;
    }
    .task-content{
        width: 150px;
    }
    .delete-btn{
        height: 40px;
        width: 40px;
    }
    .delete-img{
        height: 25px;
        width: 20px;
    }
}
@media only screen and (max-width: 940px){
    .task-content{
        width: 400px;
    }
    .time{
        font-size: 22px;
    }
    .title{
        font-size: 20px;
    }
}
@media only screen and (max-width: 480px){
    .task-content{
        width: 300px;
    }
}
@media only screen and (max-width: 370px){
    .task-content{
        width: 200px;
    }
    .time{
        font-size: 16px;
    }
    .title{
        font-size: 14px;
    }
}
</style>
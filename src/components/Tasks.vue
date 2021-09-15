<template>
  <div class="tasks">
      <div class="tasks-content">
          <p class="quick-info" v-if="tasksLength(tasks)">There is nothin planned for this day...</p>
          <ul v-else>
              <li v-for="task in tasks" :key="task.id"><Task :task="task" @taskToDelete="taskToDelete($event)" @isOpened="isOpened($event)" @taskInfo="taskInfo($event)"/></li>
          </ul>
      </div>
      <div class="task-info">
          <div class="title-info">
              <p> <span>Title:</span>{{this.singleTitle}}</p>
              <p><span>Time:</span> {{this.singleTime}}</p>
          </div>
          <div class="text-info">
              <p>{{this.singleText}}</p>
          </div>
          <button class="close-info-btn" @click="closeInfo()">CLOSE</button>
      </div>
  </div>
</template>

<script>
import Task from './Task.vue'
export default {
    components:{
        Task,
    },
    props:{
        formId: String,
        tasks: Array,
    },
    data(){
        return{
            showInfo: false,
            singleTask: false,
            singleTitle: '',
            singleTime: '',
            singleText: '',
        }
    },
    methods:{
        tasksLength(n){
            if(n.length>0){
                return false;
            }else{
                return true;
            }
        },
        taskToDelete(n){
            this.$emit('taskToDelete', n);
        },
        isOpened(n){
            if(n===false){
                    document.querySelector('.tasks-content').style.display="none"
                    document.querySelector('.task-info').style.display="flex"
            }
        },
        closeInfo(){
            this.singleTask=false;
            document.querySelector('.tasks-content').style.display="flex"
            document.querySelector('.task-info').style.display="none"
        },
        taskInfo(task){
            console.log(task);
           if(task){
               this.singleTitle=task.title;
               this.singleTime=task.time;
               this.singleText=task.text;
           }
        }
    },
    mounted(){
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
.task-info{
    height: 100%;
    width: 90%;
    background: white;
    display: none;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
    border-radius: 50px;
}
.title-info{
    height: 20%;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #333456;
    font-family: 'Montserrat', sans-serif;
    font-size: 22px;
    flex-direction: column;
}
.title-info p{
    width: 100%;
    text-align: center;
    border-bottom: 2px solid #060930;
}
.title-info span{
    color: #333456;
    font-family: 'Montserrat', sans-serif;
    font-size: 26px;
    color: #060930;
    font-weight: bold;
    padding: 0px 5px;
}
.text-info{
    height: 70%;
    width: 100%;
    font-family: 'Montserrat', sans-serif;
    font-size: 18px;
    color: #333456;
    text-align: center;
    overflow: auto;
}
.close-info-btn{
    background-color: transparent;
    border: none;
    font-size: 16px;
    color: #060930;
    cursor: pointer;
}
.tasks{
    height: 400px;
    width: 100%;
    border-bottom-left-radius: 50px;
    border-bottom-right-radius: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.tasks-content{
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    flex-direction: column;
}
.tasks-content ul{
    height: 100%;
    width: 100%;
    list-style: none;
    overflow-y: scroll;
    background-color: #333456;
}
.tasks-content ul::-webkit-scrollbar{
    width: 5px;
    background-color: white;
    cursor: pointer;
}
.tasks-content ul::-webkit-scrollbar-thumb {
  background: #F4ABC4;
}
.tasks-content ul li{
    width: 100%;
    height: 70px;
    padding: 20px 0px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-bottom: 0.5px solid white;
}
.quick-info{
    width: 100%;
    height: 80px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Montserrat', sans-serif;
    color: white;
    font-weight: 400;
}
.tasks-formula{
    height: 100%;
    width: 100%;
    background-color: grey;
    display: flex;
    justify-content: center;
    align-items: flex-start;
}
@media only screen and (max-width: 1100px){
    .tasks{
        height: 420px;
    }
    .add-btn{
        height: 40px;
        width: 40px;
    }
    .add-img{
        height: 25px;
        width: 25px;
    }
    .tasks-content{
        height: 350px;
    }
    .task-info{
        height: 350px;
    }
    .title-info{
        font-size: 18px;
    }
    .title-info span{
        font-size: 18px;
    }
    .text-info{
        font-size: 16px;
    }
}
@media only screen and (max-width: 940px){
    .tasks{
        height: 60%;
        width: 100%;
        justify-content: flex-start;
    }
    .tasks-content{
        height: 100%;
    }
    .tasks-content ul::-webkit-scrollbar{
        width: 10px;
    }
    .title-info{
        flex-direction: row;
    }
    .title-info p{
        width: 40%;
    }
}
@media only screen and (max-width: 420px){
     .title-info{
        font-size: 14px;
    }
    .title-info span{
       font-size: 14px;
    }
    .text-info{
        font-size: 14px;
    }
}
@media only screen and (max-width: 324px){
    .close-info-btn{
        font-size: 12px;
    }
     .title-info{
        font-size: 12px;
    }
    .title-info span{
       font-size: 12px;
    }
    .text-info{
        font-size: 12px;
    }
}

</style>
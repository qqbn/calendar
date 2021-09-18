<template>
  <div class="add-task">
      <div class="add-task-content">

        <div class="add-task-form">

            <div class="add-task-title">
              <input class="set-title" type="text" placeholder="Set title" v-model="taskTitle">
            </div>

            <div class="add-task-text">
              <textarea class="text" name="note" id="note" cols="30" rows="10" placeholder="Type sth here..." v-model="taskText"></textarea>
            </div>

        </div>

        <div class="add-task-time">
          <input class="time-input" type="time" v-model="timeValue">
        </div>

      </div>

      <div class="add-task-footer">
          <input type="submit" class="save-btn" value=" " @click="addTask">
      </div>

  </div>
</template>

<script>
export default {
props:{
  formId: String,
},
data(){
  return{
    isOpened: false,
    tasks: [],
    taskTitle: null,
    taskText: null,
    timeValue: null,
  }
},
methods:{
  addTask(){
    if(localStorage.getItem('tasks')){
      this.tasks=JSON.parse(localStorage.getItem('tasks'));
    }
    const string =this.taskTitle;

    if(string != null){
      if(string.length>15){
        confirm('Max length of title is 10letters');
      }else if(string===""){
        confirm('Set title!');
      }else if(this.timeValue===""){
        confirm('Set time!');
      }else{
        if(this.timeValue!=null){
          this.tasks.push({
          boxId: this.formId,
          title: this.taskTitle,
          text: this.taskText,
          time: this.timeValue,
          id: Math.floor(Math.random() * 100000),
          });

          const counter=this.tasks.length;
          this.saveTasks();
          this.$emit('refreshTasks', this.tasks[counter-1]);
          this.taskTitle='';
          this.taskText='';
          this.timeValue='';
        }
        else{
          confirm('Set time!');
        }
      }
    }else{
      confirm('Set title!');
    }
  },
  saveTasks(){
      const parsed = JSON.stringify(this.tasks);
      localStorage.setItem('tasks', parsed);
    },
},
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
.add-task{
    display: flex;
    height: 500px;
    width: 100%;
    justify-content: space-around;
    flex-direction: column;
    align-items: center;
}
.add-task-content{
  width: 100%;
  height: 85%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  flex-direction: column;
}
.add-task-form{
  height: 350px;
  width: 300px;
  background-color: white;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.add-task-title{
  width: 100%;
  height: 20%;
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: 2px solid #060930;
}
.title-box{
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Montserrat', sans-serif;
  font-size: 22px;
  font-weight: bold;
  height: 100%;
  color: #060930;
  margin-right: 5px;
}
.set-title{
  height: 50px;
  border:none;
  border-radius: 50px;
  color: #060930;
  text-align: center;
  font-weight: bold;
  background-color: #fcf7f9;
}
.set-title:hover{
  background-color: #F4ABC4;
}
.text{
  width: 100%;
  height: 100%;
  border:none;
  font-size: 18px;
  font-family: 'Montserrat', sans-serif;
  cursor: pointer;
  background-color: #fcf7f9;
  text-align: center;
  overflow-y: auto;
  resize: none;
}
.text::-webkit-scrollbar{
  width: 10px;
  background-color: white;
  cursor: pointer;
}
.text::-webkit-scrollbar-thumb{
  background-color: #060930;
}
.text:hover{
  background-color: #F4ABC4;
}
.add-task-text{
  width: 100%;
  height: 80%;
}
.time-input{
  height: 50px;
  width: 300px;
  cursor: pointer;
  border:none;
  font-family: 'Montserrat', sans-serif;
  text-align: center;
  font-size: 18px;
  border-bottom-left-radius: 20px;
  border-bottom-right-radius: 20px;
  border-top: 2px solid #060930;

}
.add-task-footer{
  width: 100%;
  height: 15%;
  border-bottom-left-radius: 50px;
  border-bottom-right-radius: 50px;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.save-btn{
  height: 40px;
  width: 40px;
  border-radius: 50%;
  border: none;
  background: url("../assets/add.svg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  cursor: pointer;
}
.cancel-btn{
  height: 50px;
  width: 50px;
  border-radius: 50%;
  border: none;
  background-color: #f76d6d;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.cancel-img{
  height: 35px;
  width: 35px;
}
.submit-box{
  height: 50px;
  width: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  background-color: white;
  border-radius: 50%;
}
@media only screen and (max-width: 1100px){
  .add-task-form{
    width: 80%;
  }
  .add-task-form{
    height: 300px;
  }
  .time-input{
    width: 240px;
  }
  .save-btn{
    height: 30px;
    width: 30px;
  }
}
@media only screen and (max-width: 940px){
  .add-task-form{
    flex-direction: row;
    height: 70%;
    width: 80%;
    border-radius: 0px;
    justify-content: space-around;
    align-items: center;
    height: 100%;
    background: #333456;
  }
  .add-task-content{
    flex-direction: row;
    height: 70%;
    width: 100%;
  }
  .add-task-footer{
    height: 10%;
    width: 100%;
    border-radius: 0;
  }
  .add-task-time{
    width: 20%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #333456;
  }
  .add-task{
    height: 70%;
    width: 100%;
  }
  .save-btn{
    height: 30px;
    width: 30px;
  }
  .add-task-title{
    border:none;
    height: 100%;
    border-radius: 0;
    width: 30%;
  }
  .add-task-text{
    height: 100%;
    width: 70%;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 0;
}
  .text{
    border-radius: 5px;
    width: 80%;
    font-size: 14px;
  }
  .submit-box{
    height: 40px;
    width: 40px;
  }
  .cancel-btn{
    height: 40px;
    width: 40px;
  }
  .time-input{
    border-radius: 50px;
  }
}
@media only screen and (max-width: 750px){
  .set-title{
    width: 150px;
  }
  .time-input{
    width: 100px;
  }
}
@media only screen and (max-width: 660px){
  .set-title{
   width: 100px;
   border-radius: 10px;
  }
  .time-input{
    border-radius: 10px;
  }
}
@media only screen and (max-width: 400px){
  .add-task-text{
    width: 50%;
    height: 100%;
  }
  .time-input{
    border-radius: 10px;
    font-size: 14px;
}
}
</style>
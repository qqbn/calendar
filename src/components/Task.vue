<template>
  <div class="task">
      <div class="task-content"> <p class="time">12:00</p> <p class="title">Shopping</p> </div>
      <button class="delete-btn"><img class="delete-img" src="../assets/trash.svg" alt="thrash"></button>
  </div>
</template>

<script>
export default {

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
.task{
    width: 100%;
    height: 50px;
    display: flex;
    justify-content: space-around;
    align-items: center;
}
.task-content{
    width: 200px;
    background: white;
    height: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    border-radius: 50px;
    cursor: pointer;
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
    font-size: 18px;
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
        font-size: 18px;
    }
    .title{
        font-size: 16px;
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
}
</style>
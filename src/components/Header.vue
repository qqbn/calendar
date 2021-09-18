<template>
  <div class="header">

      <div class="left-header">
        <button @click="monthLess()" class="left-arrow-button"><img class="left-arrow" src="../assets/right-arrow.svg" alt="arrow"></button>
        <h1>{{monthName}}</h1>
        <button @click="nextMonth()" class="right-arrow-button"><img class="right-arrow" src="../assets/right-arrow.svg" alt=""></button>
      </div>

      <div class="right-header">
          <button @click="prevYear()" class="left-arrow-button"><img class="left-arrow" src="../assets/right-arrow.svg" alt="arrow"></button>
          <h2>{{year}}</h2>
          <button @click="nextYear()" class="right-arrow-button"><img class="right-arrow" src="../assets/right-arrow.svg" alt=""></button>
      </div>

  </div>
</template>

<script>
export default {
props:{
    monthName: String,
    year: Number,
},
data(){
    return{
        monthCounter: 1,
        yearCounter: 1,
    }
},
methods:{
    monthLess(){
        this.$emit('subMonthCounter',this.monthCounter);
    },
    nextMonth(){
        this.$emit('addMonthCounter',this.monthCounter);
    },
    prevYear(){
        this.$emit('prevYear',this.yearCounter);
    },
    nextYear(){
        this.$emit('nextYear',this.yearCounter);

    }
}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
.header{
    width: 100%;
    height: 100px;
    border-radius: 50px;
    display: flex;
    justify-content: space-around;
    align-items: center;

}
.left-header{
    height: 100%;
    width: 70%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    font-family: 'Montserrat', sans-serif;
    color: #060930;
    font-size: 26px;
}
.left-arrow-button, .right-arrow-button{
    height: 50px;
    width: 50px;
    border-radius: 50px;
    border: none;
    display: flex;
    justify-content: center;
    align-items: center;
    background: white;
    box-shadow: 0px 2px 5px #060930;
    cursor: pointer;
}
.left-arrow-button:hover, .right-arrow-button:hover{
    background: #ebebeb;
}
.right-arrow{
    transform: rotate(180deg);
}
.right-header{
    height: 100%;
    width: 30%;
    border-radius: 50px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    font-size: 26px;
    font-family: 'Montserrat', sans-serif;
    color: #060930;
}
h1{
    font-weight: 400;
}
h2{
    font-weight: 400;
}
@media only screen and (max-width: 1100px){
    .left-arrow-button{
        height: 40px;
        width: 40px;
    }
    .left-arrow{
        height: 30px;
        width: 30px;
    }
    .right-arrow-button{
        height: 40px;
        width: 40px;
    }
    .right-arrow{
        height: 30px;
        width: 30px;
    }
    h1{
        font-size: 48px;
    }
    h2{
        font-size: 36px;
    }
}
@media only screen and (max-width: 940px){
    .header{
        height: 15%;
        width: 100%;
        border-radius: 0%;
        margin: 0;
        padding: 0;
    }
}
@media only screen and (max-width: 550px){
    h1{
        font-size: 42px;
    }
    h2{
        font-size: 32px;
    }
    .right-arrow-button{
        height: 35px;
        width: 35px;
    }
    .left-arrow-button{
        height: 35px;
        width: 35px;
    }
    .left-arrow, .right-arrow{
        height: 20px;
        width: 20px;
    }
}@media only screen and (max-width: 480px){
    h1{
        font-size: 36px;
    }
    h2{
        font-size: 26px;
    }
    .left-arrow-button, .right-arrow-button{
        background: transparent;
        box-shadow: none;
    }
}
@media only screen and (max-width: 370px){
     h1{
        font-size: 28px;
    }
    h2{
        font-size: 20px;
    }
}
</style>
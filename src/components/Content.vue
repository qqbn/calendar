<template>
  <div class="content">
      <div class="days">
          <div class="day">Mon</div>
          <div class="day">Tue</div>
          <div class="day">Wed</div>
          <div class="day">Thu</div>
          <div class="day">Fri</div>
          <div class="day">Sat</div>
          <div class="day">Sun</div>
      </div>
      <ul class="list">
        <div class="single-row" v-for="week in newMonth" :key="week.id">
            <li class="single-day" v-for="day in week" :key="day.id"> <SingleDay :day="day"/></li>
        </div>
      </ul>
  </div>
</template>

<script>
import SingleDay from './SingleDay.vue'
export default {
props: ['newMonth'],
components:{
    SingleDay,
}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
.content{
    width: 100%;
    height: 550px;
    border-bottom-left-radius: 50px;
    border-bottom-right-radius: 50px;
}
.days{
    width:100%;
    height: 50px;
    display: flex;
    justify-content: space-around;
    align-items: center;
}
.day{
    height: 100%;
    width: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Montserrat', sans-serif;
    color: #060930;
    font-size: 30px;
    font-weight: 600;
    text-decoration: 4px underline #F4ABC4;
}
.list{
    width: 100%;
    height: 550px;
    border-bottom-left-radius: 50px;
    border-bottom-right-radius: 50px;
    list-style: none;
}
.single-row{
    height: 80px;
    width: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
}
.single-day{
    display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  font-family: 'Montserrat', sans-serif;
  font-size: 24px;
  font-weight: 400;
  width: 100px;
}
@media only screen and (max-width: 1100px){
    .content{
        height: 450px;
    }
    .single-row{
        height: 50px;
    }
    .list{
        height: 450px;
    }
}
@media only screen and (max-width: 940px){
    .content{
        height: 85%;
        width: 100%;
        border-bottom-left-radius: 0px;
        border-bottom-right-radius: 0px;
        justify-content: space-around;
    }
    .list{
        height: 80%;
    }
}
@media only screen and (max-width: 550px){
    .day{
        font-size: 26px;
        width: 50px;
    }
}
@media only screen and (max-width: 480px){
    .day{
        font-size: 22px;
    }
}
@media only screen and (max-width: 370px){
    .day{
        font-size: 18px;
    }
    .single-day{
        width: 30px;
    }
}
@media only screen and (max-height: 700px){
    .single-row{
        height: 50px;
    }
}
@media only screen and (max-height: 500px){
.single-row{
        height: 40px;
    }
}
@media only screen and (max-height: 400px){
    .single-row{
        height: 25px;
    }
}
</style>
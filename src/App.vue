<template>
  <div class="main-box">
    <Calendar :newMonth="newMonth" :monthName="monthName" :year="year" @subMonthCounter="subMonthCounter($event)" @addMonthCounter="addMonthCounter($event)"/>
    <FormulaBox />
  </div>
</template>

<script>
import Calendar from './components/Calendar.vue'
import FormulaBox from './components/FormulaBox.vue'

export default {
  name: 'App',
  components: {
    Calendar,
    FormulaBox
  },
  data(){
    return{
      weekday: ["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"],
      monthNames: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
      year: null,
      month: null,
      date: new Date(),
      firstDay: null,
      lastDay: null,
      counter: null,
      newDays: [],
      singleMonth:[],
      newWeek:[],
      newMonth:[],
      monthBefore: null,
      yearBefore: null,
      daysMonthBefore: [],
      daysMonthNext: [],
      monthName: null,
    }
  },
  methods:{
     daysInMonth (month, year) {
      return new Date(year, month, 0).getDate();
    },

    getDaysFromNextMonth(month){
      if(month==11){
        this.yearBefore=this.year+1;
        this.monthBefore=0;
      }else{
        this.yearBefore=this.year;
        this.monthBefore=month+1;
      }
      this.counter=this.daysInMonth(this.monthBefore+1,this.yearBefore);
      for(let i=1;i<=this.counter;i++){
         this.firstDay =new Date(this.yearBefore,this.monthBefore,i);
        this.daysMonthNext.push(this.firstDay.getDate());
      }
    },

    getDaysFromLastMonth(month){
      if(month==0){
        this.yearBefore=this.year-1;
        this.monthBefore=11;
      }else{
        this.yearBefore=this.year;
        this.monthBefore=month-1;
      }
      this.counter=this.daysInMonth(this.monthBefore+1,this.yearBefore);
      for(let i=1;i<=this.counter;i++){
        this.firstDay =new Date(this.yearBefore,this.monthBefore,i);
        this.daysMonthBefore.push(this.firstDay.getDate());
      }
    },

    getMonthName(month){
     this.monthName=this.monthNames[month];
    },

    getMonth(){
        this.sortMonth();
        this.convertMonth();
        this.getDaysFromLastMonth(this.month);
        this.getDaysFromNextMonth(this.month);
        this.mergeMonth();
        console.log(this.newMonth);
        this.getMonthName(this.month);
    },

     subMonthCounter(month){
         this.month=this.month-month;
         if(this.month<0){
           this.month=11;
           this.year=this.year-1;
         }
          this.newMonth=[];
          this.singleMonth=[];
          this.newDays=[];
          this.newWeek=[],
          this.daysMonthBefore= [],
          this.daysMonthNext= [],
          this.getMonth();
    },
    addMonthCounter(counter){
      this.month=this.month+counter;
         if(this.month>11){
           this.month=0;
           this.year=this.year+1;
         }
          this.newMonth=[];
          this.singleMonth=[];
          this.newDays=[];
          this.newWeek=[],
          this.daysMonthBefore= [],
          this.daysMonthNext= [],
          this.getMonth();
    },

    sortMonth(){
      this.firstDay= new Date(this.year,this.month);
      this.counter=this.daysInMonth(this.month+1,this.year);
      for(let i=1;i<=this.counter;i++){
        this.firstDay= new Date(this.year,this.month,i);
        const index=this.firstDay.getDay();
        this.newDays.push(index);
        if(index==0){
          this.singleMonth.push(this.newDays);
          this.newDays=[];
        }
      }
      this.singleMonth.push(this.newDays);
    },

    convertMonth(){
      let yay=1;
      this.singleMonth.forEach(element => {
          element.forEach(element => {
            element=yay;
            this.newWeek.push(element);
            yay++;
          });
          this.newMonth.push(this.newWeek);
          this.newWeek=[];
        });
    },

    mergeMonth(){
      if(this.newMonth[0].length<7){
          this.daysMonthBefore.reverse();
          this.daysMonthBefore.forEach(element => {
             if(this.newMonth[0].length<7)
            this.newMonth[0].unshift(element);
          });
        }
        this.newMonth.forEach(element => {
          if(element.length<7){
          this.daysMonthNext.forEach(test => {
            if(element.length<7){
               element.push(test);
            }
          });
        }
        });
    }
  },
  mounted(){
    this.year=this.date.getFullYear();
    this.month= this.date.getMonth();
    this.getMonth();
  }
}
</script>

<style>
*{
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
.main-box{
 height: 100vh;
 width: 100%;
 background: white;
 display: flex;
 justify-content: space-around;
 align-items: center;
}
@media only screen and (max-width: 940px){
  .main-box{
    height: 100vh;
    flex-direction: column;
    justify-content: center;
    margin-top: 0;
  }
}
</style>

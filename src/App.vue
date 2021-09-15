<template>
  <div class="main-box">
    <Calendar :newMonth="newMonth"
    :monthName="monthName"
    :year="year"
    @subMonthCounter="subMonthCounter($event)"
    @addMonthCounter="addMonthCounter($event)"
    @prevYear="prevYear($event)"
    @nextYear="nextYear($event)"
    @chosenDay="chosenDay($event)"
    @boxId="boxId($event)"
    @singleDayTasks="singleDayTasks($event)"
    :formId="formId"
    :dotsArr="dotsArr"
    />
    <FormulaBox
    @refreshTasks="refreshTasks($event)"
    :boxMonth="boxMonth"
    :day="todaysDay"
    :year="year"
    :formId="formId"
    :tasks="tasks"
     @colorBox="colorBox($event)"
     @taskToDelete="taskToDelete($event)"
    />
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
      todaysDay: null,
      boxMonth: null,
      formId: null,
      tasks: [],
      testArr: [],
      dotsArr:[],
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
        // this.daysMonthNext.push(this.firstDay.getDate());
        this.daysMonthNext.push(0);
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
        // this.daysMonthBefore.push(this.firstDay.getDate());
        this.daysMonthBefore.push(0);
      }
    },

    getMonthName(month){
      return this.monthNames[month];
    },

    getMonth(){
        this.sortMonth();
        this.convertMonth();
        this.getDaysFromLastMonth(this.month);
        this.getDaysFromNextMonth(this.month);
        this.mergeMonth();
        this.monthName=this.getMonthName(this.month);
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

    prevYear(yearCounter){
      this.year=this.year-yearCounter;
      this.newMonth=[];
      this.singleMonth=[];
      this.newDays=[];
      this.newWeek=[],
      this.daysMonthBefore= [],
      this.daysMonthNext= [],
      this.getMonth();
    },

    nextYear(yearCounter){
      this.year=this.year+yearCounter;
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
        // console.log(this.newMonth);
    },

    chosenDay(day){
      this.todaysDay=day;
      this.boxMonth=this.getMonthName(this.month);
    },

    boxId(n){
        this.formId=n;
    },

    singleDayTasks(n){
      this.tasks=[],
      this.tasks=n;
    },

     refreshTasks(m){
       this.tasks.push(m);
    },

    getStartingData(){
        if(localStorage.getItem('tasks')){
        this.testArr=JSON.parse(localStorage.getItem('tasks'));
        }
        if(this.testArr.length>0){
            this.testArr.forEach(element => {
              if(element.boxId===this.formId){
                this.tasks.push(element);
                }
            });
            console.log(this.tasks);
        }
    },

    newTask(n){
      this.tasks.push({
        boxId: n.formId,
        title: n.taskTitle,
        text: n.taskText,
        time: n.timeValue,
        id: n.id,
      });
    },

    getDays(){
      // console.log(this.testArr);
      this.testArr.forEach(element => {
        this.dotsArr.push(element.boxId);
      });
      // console.log(this.dotsArr);
    },

    colorBox(n){
      this.dotsArr.push(n);
      // console.log(this.dotsArr);
    },
    taskToDelete(n){
      console.log(n);
      if(localStorage.getItem('tasks')){
        this.testArr=JSON.parse(localStorage.getItem('tasks'));
      }
      this.testArr.forEach(element => {
        if(element.id===n.id){
          console.log('jest taki element');
          const index=this.testArr.indexOf(element);
          if (index > -1) {
            this.testArr.splice(index, 1);
          }
        }
      });
      console.log(this.testArr);
      const parsed = JSON.stringify(this.testArr);
      localStorage.setItem('tasks', parsed);
      this.tasks=[];
      if(this.testArr.length>0){
        this.testArr.forEach(element => {
          if(element.boxId===this.formId){
              this.tasks.push(element);
          }
        });
      }
    }
  },

  mounted(){
    this.todaysDay=new Date().getDate();
    this.year=this.date.getFullYear();
    this.month= this.date.getMonth();
    this.getMonth();
    this.boxMonth=this.getMonthName(this.month);
    this.formId=this.todaysDay+this.monthName+this.year;
    console.log(this.formId);
    this.getStartingData();
    this.getDays();
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

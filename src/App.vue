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
      tmpMonth: null,
      tmpDay: null,
      textUnderline: null,
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

        this.daysMonthNext.push({
          day: 0,
          task: false,
        });
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
        this.daysMonthBefore.push({
          day: 0,
          task: false,
        });
      }
    },

    getMonthName(month){
      return this.monthNames[month];
    },

    dotsFunc(){
      this.testArr.forEach(element => {
        this.tmpMonth=element.boxId.replace(/[0-9]/g, '');
        this.tmpDay=element.boxId.match(/\d/g);
        this.tmpDay=this.tmpDay.join("")
          this.dotsArr.push({
            day: this.tmpDay,
            month: this.tmpMonth,
          })
      });
    },

    checkDays(){
      this.dotsArr.forEach(dot => {
        this.newMonth.forEach(element => {
          element.forEach(day => {
            if((day.day+""+this.year)===dot.day && this.monthName==dot.month){
              day.task=true;
            }
          });
        });
      });
    },

    getMonth(){
      this.sortMonth();
      this.convertMonth();
      this.getDaysFromLastMonth(this.month);
      this.getDaysFromNextMonth(this.month);
      this.mergeMonth();
      this.monthName=this.getMonthName(this.month);
      this.dotsFunc();
      this.checkDays();
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
      this.dotsArr=[];
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
      this.dotsArr=[];
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
      this.dotsArr=[];
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
      this.dotsArr=[];
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
          this.newWeek.push({
            day: element,
            task: false,
            dayId: element+""+this.getMonthName(this.month)+""+this.year,
            activeTab: false,
          });
          yay++;
        });
      this.newMonth.push(this.newWeek);
      this.newWeek=[];
      });

        // console.log(this.newMonth);
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
    },

    chosenDay(day){
      this.todaysDay=day;
      this.boxMonth=this.getMonthName(this.month);
    },

    boxId(n){
        this.formId=n;

        this.newMonth.forEach(week => {
          week.forEach(element => {
            if(element.activeTab==true){
              element.activeTab=false;
            }
          });
        });

        this.newMonth.forEach(week => {
          week.forEach(element => {
            if(element.dayId===this.formId){
              element.activeTab=true;
            }
          });
        });
    },

    singleDayTasks(n){
      this.tasks=[],
      this.tasks=n;
    },

    refreshTasks(m){
      this.tasks.push(m);
      this.dotsArr=[];

      if(localStorage.getItem('tasks')){
        this.testArr=JSON.parse(localStorage.getItem('tasks'));
      }

      this.dotsFunc();
      this.checkDays();
    },

    getStartingData(){

      if(localStorage.getItem('tasks')){
        this.testArr=JSON.parse(localStorage.getItem('tasks'));
      }

      if(this.testArr.length>0){
        this.testArr.forEach(element => {
          if(element.boxId===this.formId){
            console.log('weszlo');
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

    taskToDelete(n){

      if(localStorage.getItem('tasks')){
        this.testArr=JSON.parse(localStorage.getItem('tasks'));
      }

      this.testArr.forEach(element => {

        if(element.id===n.id){
          const index=this.testArr.indexOf(element);

          if (index > -1) {
            this.testArr.splice(index, 1);
          }
        }

      });

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

      this.dotsArr=[];
      this.newMonth=[];
      this.singleMonth=[];
      this.newDays=[];
      this.newWeek=[],
      this.daysMonthBefore= [],
      this.daysMonthNext= [],
      this.getMonth();
      this.dotsFunc();
      this.checkDays();
    }
  },

  mounted(){
    this.todaysDay=new Date().getDate();
    this.year=this.date.getFullYear();
    this.month= this.date.getMonth();
    this.boxMonth=this.getMonthName(this.month);
    this.formId=this.todaysDay+this.boxMonth+this.year;
    this.getStartingData();
    this.getMonth();
    console.log(this.formId);

    this.newMonth.forEach(week => {
      week.forEach(element => {
        if(element.dayId===this.formId){
            element.activeTab=true;
        }
      });
    });
  },
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

<template>
  <p @click="openBox(day)" class="single-day-number" :class="{fillday:isTask}" :id="this.dayId" v-if="isNull(day)">{{ day }}</p>
</template>

<script>
export default {
  props:{
    day: Number,
    year: Number,
    monthName: String,
    formId: String,
    dotsArr: Array,
  },
  data(){
    return{
      dayId: '',
      oldId: null,
      newId: null,
      tasks: [],
      singleDayTasks: [],
      isTask: false,
    }
  },
  methods:{
    openBox(n){
      this.tasks=[];
      this.singleDayTasks=[];
      this.dayId=n+this.monthName+this.year;
      // const test=document.getElementById(`${this.dayId}`);
      // console.log(test);
      this.$emit('chosenDay', this.day);
      this.$emit('boxId', this.dayId);
       if(localStorage.getItem('tasks')){
            this.tasks=JSON.parse(localStorage.getItem('tasks'));
        }
         if(this.tasks.length>0){
                 this.tasks.forEach(element => {
                    if(element.boxId===this.dayId){
                        this.singleDayTasks.push(element);
                    }
                });
                // console.log(this.singleDayTasks);
                this.$emit('singleDayTasks', this.singleDayTasks);
            }
    },
    isNull(n){
      if(n===0){
        return false
      }
      else{
        return true
      }
    },
  },
  mounted(){

  },
  updated(){
    // this.dayId=this.day+this.monthName+this.year;
    // console.log(this.dayId);
    // this.dotsArr.forEach(element => {
    //  if(element===this.dayId){
    //      this.isTask=true;
    //    }
    // });
  },
}
</script>

<style>
.single-day-number{
    width: 50px;
    height: 50px;
    font-weight: bold;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
}
.single-day-number:hover{
    background: #F4ABC4;
    cursor: pointer;
}
.fillday{
  background: #F4ABC4;
}
.new-bck{
  background-color: #595B83;
}
.old-bck{
  background-color: transparent;
}
.got-tasks{
  background-color: #F4ABC4;
}
@media only screen and (max-width: 480px){
  .single-day-number{
    font-size: 22px;
  }
}
@media only screen and (max-width: 370px){
  .single-day-number{
    font-size: 18px;
  }
}
@media only screen and (max-height: 400px){
  .single-day-number{
    font-size: 12px;
  }
  .single-day-number{
    height: 30px;
    width: 30px;
  }
}
</style>
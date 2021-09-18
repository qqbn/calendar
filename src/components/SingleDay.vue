<template>
  <p @click="openBox(day.day)" class="single-day-number" :class="{fillday:isTask, selectedDay:oldId}" :id="this.dayId" v-if="isNull(day.day, day.task, day.activeTab)">{{ day.day }}</p>
</template>

<script>
export default {
  props:{
    day: Object,
    year: Number,
    monthName: String,
    formId: String,
  },
  data(){
    return{
      dayId: '',
      oldId: false,
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
      this.$emit('chosenDay', this.day.day);
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

          this.$emit('singleDayTasks', this.singleDayTasks);
        }
    },

    isNull(n,m,z){
      if(n===0){
        return false
      }
      else{

        if(m===true){
          this.isTask=true;
        }else{
          this.isTask=false;
        }

        if(z==true){
          this.oldId=true;
        }else{
          this.oldId=false;
        }

        return true

      }
    },
  },
  mounted(){
  },
  updated(){
  },
}
</script>

<style>
.selectedDay{
  background-color: #595B83 !important;
}
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
    background: #595B83;
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
    height: 30px;
    width: 30px;
  }
}
@media only screen and (max-height: 400px){
  .single-day-number{
    height: 30px;
    width: 30px;
    font-size: 12px;
  }
}
</style>
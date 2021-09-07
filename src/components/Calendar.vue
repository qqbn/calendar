<template>
    <div class="calendar">
        <Header :monthName="monthName" :year="year" @subMonthCounter="subMonthCounter($event)" @addMonthCounter="addMonthCounter($event)" @prevYear="prevYear($event)" @nextYear="nextYear($event)"/>
        <Content :newMonth="newMonth" @chosenDay="chosenDay($event)"/>
    </div>
</template>

<script>
import Header from './Header.vue'
import Content from './Content.vue'
export default {
name: 'Calendar',
props:{
    newMonth: Array,
    monthName: String,
    year: Number,
},
components:{
    Header,
    Content,
},
methods:{
    subMonthCounter(monthCounter){
        this.$emit('subMonthCounter', monthCounter)
    },
    addMonthCounter(monthCounter){
        this.$emit('addMonthCounter', monthCounter)
    },
    prevYear(yearCounter){
        this.$emit('prevYear',yearCounter);
    },
    nextYear(yearCounter){
        this.$emit('nextYear', yearCounter);
    },
    chosenDay(day){
        this.$emit('chosenDay', day);
    }
}
}
</script>

<style>
.calendar{
    height: 700px;
    width: 800px;
    background: white;
    box-shadow: 1px 1px 10px 0.5px #060930;
    border-radius: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
@media only screen and (max-width: 1255px){
    .calendar{
        width: 700px;
    }
}
@media only screen and (max-width: 1100px){
     .calendar{
        width: 600px;
        height: 600px;
    }
}
@media only screen and (max-width: 940px){
    .calendar{
        height: 70vh;
        width: 100%;
        align-items: flex-start;
        border-radius: 0px;
    }
}
</style>
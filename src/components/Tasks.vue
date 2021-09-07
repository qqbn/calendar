<template>
  <div class="tasks" v-if="!returnView">
      <div class="tasks-content">
          <p class="quick-info" v-show="showInfo">There is nothin planned for this day...</p>
          <ul>
              <li><Task /></li>
              <li><Task /></li>
              <li><Task /></li>
              <li><Task /></li>
              <li><Task /></li>
              <li><Task /></li>
              <li><Task /></li>
              <li><Task /></li>
          </ul>
      </div>
  </div>
</template>

<script>
import Task from './Task.vue'
export default {
    components:{
        Task,
    },
    props:{
        returnView: Boolean,
    },
    data(){
        return{
            showInfo: false,
            show: false,
        }
    },
    methods:{
        addTask(){
            this.show=true;
            if(this.show){
                document.querySelector('.tasks').style.display="none"
            }
            this.$emit('showFormula', this.show);
        }
    },
    renderTriggered(){
        console.log(this.returnView);
        if(this.returnView==false){
            document.querySelector('.tasks').style.display="flex"
        }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
.tasks{
    height: 400px;
    width: 100%;
    border-bottom-left-radius: 50px;
    border-bottom-right-radius: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.tasks-content{
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    flex-direction: column;
}
.tasks-content ul{
    height: 100%;
    width: 100%;
    list-style: none;
    overflow-y: scroll;
    background-color: #333456;
}
.tasks-content ul::-webkit-scrollbar{
    width: 5px;
    background-color: white;
    cursor: pointer;
}
.tasks-content ul::-webkit-scrollbar-thumb {
  background: #F4ABC4;
}
.tasks-content ul li{
    width: 100%;
    height: 70px;
    padding: 20px 0px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-bottom: 0.5px solid white;
}
.quick-info{
    width: 100%;
    height: 80px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Montserrat', sans-serif;
    color: white;
    font-weight: 400;
}
.tasks-formula{
    height: 100%;
    width: 100%;
    background-color: grey;
    display: flex;
    justify-content: center;
    align-items: flex-start;
}
@media only screen and (max-width: 1100px){
    .tasks{
        height: 420px;
    }
    .add-btn{
        height: 40px;
        width: 40px;
    }
    .add-img{
        height: 25px;
        width: 25px;
    }
}
@media only screen and (max-width: 940px){
    .tasks{
        height: 60%;
        width: 100%;
        justify-content: flex-start;
        background: red;
    }
    .tasks-content{
        height: 100%;
    }
    .tasks-content ul::-webkit-scrollbar{
        width: 10px;
    }
}
@media only screen and (max-width: 370px){

}

</style>
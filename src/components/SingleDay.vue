<template>
  <p @click="openBox" class="single-day-number">{{ day }}</p>
</template>

<script>
export default {
  props:{
    day: Number,
  },
  methods:{
    openBox(){
      this.$emit('chosenDay', this.day);
    }
  }

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
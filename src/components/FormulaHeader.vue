<template>
    <div class="formula-header">
      <h3 class="formula-header-text">{{day}}-{{boxMonth}}-{{year}}</h3>
    </div>
</template>

<script>
export default {
  props:{
    boxMonth: String,
    day: Number,
    year: Number,
  }
}
</script>

<style>
.formula-header{
  width: 100%;
  height: 80px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-top-left-radius: 50px;
  border-top-right-radius: 50px;
  font-family: 'Montserrat', sans-serif;
  color: white;
}
.formula-header-text{
  font-size: 28px;
  text-decoration: 4px underline #F4ABC4;
}
@media only screen and (max-width: 1100px){
  .formula-header-text{
    font-size: 22px;
  }
  .formula-header{
    height: 50px;
  }
}
@media only screen and (max-width: 940px){
  .formula-header{
    height: 20%;
    border-top-left-radius: 0px;
    border-top-right-radius: 0px;
    width: 100%;
  }
  .formula-header-text{
    font-size: 28px;
  }
}

</style>
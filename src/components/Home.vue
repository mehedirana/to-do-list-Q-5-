<template>
  <div class="homes">
     <h1>hi i m home component</h1>
     <Screen/>
     <Screen2/>
  </div>

</template>

<script>
import Screen from './Screen';
import Screen2 from './Screen2'
export default {
 name: "Home",
 components:{
     // eslint-disable-next-line vue/no-unused-components
     Screen,
     // eslint-disable-next-line vue/no-unused-components
     Screen2
 }
}
</script>

<style scoped>
div{
    background-color: cadetblue;
  height: 300px;
}
h1{
   text-size-adjust: 20;
}
    
</style>
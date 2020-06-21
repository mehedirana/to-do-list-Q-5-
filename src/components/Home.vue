<template>
    <div>
        <h1>hello i am from home</h1>
        <h1>{{data}}</h1>
 
   </div>
</template>
 <script>
export default {
  name: 'Home',
  props:{
      data: String 
  }
};
</script>
<template>
  <div id="app" class="contrainer">
     <h1>ToDo app</h1>
     <img alt="Vue logo" src="./assets/logo.png">
     <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
     <toDoList/>
  </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import HelloWorld from './components/HelloWorld.vue';
import ToDoList from './components/ToDoList';
export default {
  name: 'App',
  components: {
    // HelloWorld,
    ToDoList
  }
}
</script>

<style>

* {
  box-sizing: border-box;
}
.contrainer{
  max-width: 500px;
   margin: 0 auto;
}
img{
  padding: 10px;
  margin-left: 140px;
}
h1{
  margin-left: 155px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
   /* text-align: center; */
  margin-top: 60px;
  font-size: 20px;
}
</style>

<template>
    <div>
        <h1>hello i am from home</h1>
        <h1>{{data}}</h1>
        <button v-on:mouseover="handle('welcome')">click me</button>
        <table>
           <tr>
             <td>id </td>
             <td>name </td>
             <td>email </td>
           </tr>

           <tr v-for="user in arr" :key="user.id">
             <td>{{user.id}}</td>
             <td>{{user.name}}</td>
             <td>{{user.email}} </td>
           </tr>
        </table>
 
   </div>
</template>
 <script>
export default {
  name: 'Home',
  props:{
      data: String 
  },methods: {
      handle(data){
          console.log("called")
          alert(data)
      }
  },data(){
      return {
          arr:[
              {id:1, name:"mehedi", email:"mehedi@gmai.com"},
              {id:2, name:"rajib", email:"rajib@gmai.com"},
              {id:3, name:"imran", email:"imran@gmai.com"},
              {id:4, name:"mashuk", email:"mashuk@gmai.com"},
          ]
      }
  }
};
</script>
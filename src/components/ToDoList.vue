<template>
    <div>
      <input type="text" class="todo-input" v-model="newTodo" @keyup.enter="addTodo" >
      <div v-for="todo in todos" :key="todo.id" class="todo-item">
          <div>
              {{todo.title}}
          </div>

         <div class="remove-item">
           &times;
         </div>
      </div>  
    </div>
</template>

<script>
export default {
    name: "ToDoList",
    data(){
        return{
            newTodo: '',
            idFortodo: 3,
            todos: [
                {
                    'id': 1,
                    'title': 'hi i am mehedi',
                    'completed': 'false',
                },
                 {
                    'id': 2,
                    'title': 'hi i am rajib',
                    'completed': 'false',
                }
            ]
        }
    },
    methods:{
        addTodo(){
            if(this.newTodo.trim().length==0) return
            this.todos.push({
               id: this.idFortodo,
               title: this.newTodo,
               completed: false, 
            })
            this.newTodo= '',
            this.idFortodo++
        }
    }
}
</script>

<style lang="scss">
.todo-input {
    width: 100%;
    padding: 10px;
    margin-bottom: 100px;
    font-size: 15px;
    /* margin-top: 200px; */
    &:focus{
        outline: 0;
    }
}
.todo-item {
        margin-bottom: 15px;
        display:  flex;
        justify-content: space-between;
        align-items: center;
    }


</style>

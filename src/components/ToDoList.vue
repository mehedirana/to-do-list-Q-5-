<template>
    <div>
      <input type="text" class="todoInput" v-model="newTodo" @keyup.enter="addTodo">
      <div v-for="todo in todos" :key="todo.id" class="todo-item">
        {{todo.title}}
      </div>
    </div>
</template>

<script>
export default {
    name: "ToDoList",
    data(){
        return{
            newTodo: '',
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
            alert("adding")
        }
    }
}
</script>

<style lan="scss" scoped>

</style>

<template>
  <div>
    <input type="text" class="todo-input" v-model="newTodo" @keyup.enter="addTodo" />
    <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
      <div class="todo-item-left">
        <div v-if="!todo.editing" @dblclick="editTodo(todo)" class="todo-item-label">{{todo.title}}</div>
        <input
          v-else
          @blur="editDone(todo)"
          @keyup.enter="editDone(todo)"
          class="todo-item-edit"
          type="text"
          v-model="todo.title"
          v-focus
          @keyup.esc="cancelEdit(todo)"
        />
      </div>

      <div class="remove-item" @click="removeTodo(index)">&times;</div>
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
            beforeEditCache: '',
            todos: [
                {
                    'id': 1,
                    'title': 'hi i am mehedi',
                    'completed': false,
                    'editing': false,
                },
                 {
                    'id': 2,
                    'title': 'hi i am rajib',
                    'completed': false,
                    'editing': false,
                },
            ]
        }
    },
  directives: {
  focus: {
    // directive definition
    inserted: function (el) {
      el.focus()
    }
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
        },
        removeTodo(index){
            alert("removing")
        this.todos.splice(index,1)
        },
        editTodo(todo){
            this.beforeEditCache = todo.title
            todo.editing = true
        },
        editDone(todo){
          todo.editing = false
        },
        cancelEdit(todo){
            todo.title = this.beforeEditCache
            todo.editing= false

        }
    }
}
</script>

<style lang="scss">
.todo-input {
  width: 100%;
  padding: 10px;
  margin-bottom: 100px;
  font-size: 20px;
  /* margin-top: 200px; */
  &:focus {
    outline: 0;
  }
}
.todo-item {
  margin-bottom: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.remove-item {
  cursor: pointer;

  &:hover {
    color: black;
  }
}
.todo-item-left {
  display: flex;
  align-items: center;
}
.todo-item-label {
  padding: 10px;
  border: 1px solid white;
  margin-left: 10px;
}
.todo-item-edit {
  font-size: 20px;
  color: #2c3e50;
  margin-left: 12px;
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  font-family: "Avenir", Helvetica, Arial, sans-serif;

  &:focus {
    outline: none;
  }
}
</style>

<template>
  <div>
    <input type="text" class="todo-input" v-model="newTodo" @keyup.enter="addTodo" />
    <div v-for="(todo, index) in todosFiltered" :key="todo.id" class="todo-item">

      <div class="todo-item-left">
        <input type="checkbox" v-model="todo.completed">
        <div v-if="!todo.editing" @dblclick="editTodo(todo)" class="todo-item-label"
         :class="{completed : todo.completed}">{{todo.title}}</div>
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
    

    <div class="extra-container">
      <div><label><input type="checkbox" :checked="!anyRemaining" @change="checkAllTodos">check all</label></div>
      <div>{{ remaining }} items left</div>
    </div>

    <div class="extra-container">
      <div>
        <button :class="{ active: filter == 'all'}" @click="filter = 'all'">All</button>
        <button :class="{ active: filter =='active'}" @click="filter = 'active'">Active</button>
        <button :class="{ active: filter == 'completed'}" @click="filter = 'completed'">Completed</button>
      </div>

      <div>
        <transition name="fade">
          <button v-if="showClearCompletedButton" @click="clearCompleted">clear completed</button>
        </transition>
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
            beforeEditCache: '',
            filter: 'all',
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
    computed: {
      remaining(){
          return this.todos.filter(todo => !todo.completed).length
      },

      anyRemaining(){
        return this.remaining != 0
      },

      todosFiltered(){
        if(this.filter == 'all'){
          //alert("from all")
          return this.todos
        }
        else if(this.filter == 'active'){
         // alert("from active")
          return this.todos.filter(todo => !todo.completed)
        }
        else if(this.filter == 'completed'){
         // alert("from completed")
          return this.todos.filter(todo => todo.completed)
        }
        
        //alert("before return todos")
        return this.todos
      },

      showClearCompletedButton(){
        return this.todos.filter(todo => todo.completed).length > 0
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
               editing: false, 
            })
            this.newTodo= '',
            this.idFortodo++
        },

        removeTodo(index){
           // alert("removing")
        this.todos.splice(index,1)
        },

        editTodo(todo){
            this.beforeEditCache = todo.title
            todo.editing = true
        },

        editDone(todo){
          if(todo.title.trim() ==''){
            todo.title = this.beforeEditCache
          }
          todo.editing = false
        },

        cancelEdit(todo){
            todo.title = this.beforeEditCache
            todo.editing= false

        },
        checkAllTodos(){
          this.todos.forEach((todo) => todo.completed = event.target.checked)
        },
        clearCompleted(){
          this.todos = this.todos.filter(todo => !todo.completed)
        }
    }
}
</script>

<style lang="scss">
.todo-input {
  width: 100%;
  padding: 10px;
  margin-bottom: 30px;
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
.completed{
       text-decoration: line-through;
       color: crimson;    
}
.extra-container{
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 16px;
  padding-top: 14px;
  margin-bottom: 14px;
  border-top: 1px solid black;
}
button{
  font-size: 15px;
  background-color: white;
  font-weight: bold;
  appearance: none;
  padding: 5px;
  margin: 10px;
  border: none;

  &:hover{
    background: rgba(47, 241, 255, 0.897);
  }
  &:focus{
    outline: none;
  }
}
 .active{
    background: rgba(47, 241, 255, 0.897);
  }
  .fade-enter-active, .fade-leave-active {
    transition: opacity .2s;
  }
</style>

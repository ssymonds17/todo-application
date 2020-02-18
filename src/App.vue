<template>
<div class="margin">
  <div class="container">
    <md-card>
      <md-card-header class="header">
        <div class="md-title">Todo List Application</div>
      </md-card-header>
      <md-card-content class="todo-box">
        <md-field>
          <md-input class="new-todo-input" v-model="currentTodo" @keydown.enter="addTodo()" placeholder="New todo item"></md-input>
        </md-field>
          <ul class="todos">
            <li class="todo-item" v-for="todo in todos" :key="todo.id">
              <span>
                <input 
                  class="completed-button" 
                  type="checkbox" 
                  v-model="todo.completed"
                  />

              <span
                v-if="!todo.edit"
                class="todo-item-label"
                :class='{ completed: todo.completed }'
                @dblclick="editTodo(todo)"
                >{{ todo.label }}
              </span>

              <div v-if="todo.edit">
                <md-field>
                  <md-input 
                    class="todo-item-edit"
                    type="text" 
                    v-model='todo.label'
                    @keyup.enter="completedEdit(todo)"
                    @keyup.esc="completedEdit(todo)"
                    @focusout="completedEdit(todo)"
                    placeholder="Edit todo"
                  ></md-input>
                </md-field>
              </div>
            </span>

              <span class="actions">
                <md-button class="edit-button" @click="editTodo(todo)">
                  <md-icon>edit</md-icon>
                </md-button>
                <md-button class="delete-button" @click="removeTodo(todo)">
                  <md-icon>delete</md-icon>
                </md-button>
              </span>
            </li>
          </ul>
        </md-card-content>
      </md-card>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: '',
      editedTodo: null
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length, 
        label: this.currentTodo, 
        completed: false,
        edit: false
        });
      this.currentTodo = '';
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    check(todo) {
      todo.completed =  !todo.completed;
    },
    editTodo(todo) {
      todo.edit = true;
    },
    completedEdit(todo) {
      todo.edit = false;
    }
  }
}
</script>

<style>

li {
  list-style: none;
}

ul {
  margin: 0;
  padding: 0;
}

.margin {
  margin: 20px;
}

.container {
  margin: auto;
  padding-top: 15px;
  text-align: center;
  width: 50%;
  border: solid;
}

.completed {
  text-decoration: line-through;
  color: lightgray;
}

.todo-box {
  font-size: 1.5em;
  padding: 0px 5px 2px 5px;
}

.todo-item {
  margin-top: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 0.1px solid;
  border-color: lightgray;
}

.todo-item-label {
  margin-left: 10px;
}

.delete-button:hover {
  cursor: pointer;
}

.todos {
  margin: 10px;
}

.new-todo-input {
  width: 100px;
  text-align: center;
}

.completed-button {
  margin-left: 20px;
  float: left;
}

.edit-button {
  color: #589167;
  margin-right: 20px;
}

.delete-button {
  color: #da4302;
  margin-right: 20px;
}

.completed-button:hover {
  cursor: pointer;
}

.edit-button:hover {
  cursor: pointer;
}

</style>
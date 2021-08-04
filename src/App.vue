<template>
  <html>
    <div class="flex">
      <div class="widht35"></div>
      <div>
        <h1 class="todoApp">Todo App com alteração</h1>
        <p class="novotodo">Novo Todo</p>
        <input
          class="input"
          type="text"
          v-model="newTodo"
          @keyup.enter="addTodo()"
        />
        <div>
          <input
            class="buttonAdd"
            type="button"
            value="Adicionar"
            @click="addTodo()"
          />
        </div>

        <div class="flex2 border borda">
          <h1 class="todolist">Todo List</h1>
          <input
            class="buttonRemove"
            type="button"
            value="Remover todos"
            @click="remove()"
          />
        </div>
        <div>
          <h2 class="todolist2">Fazendo</h2>
        </div>
        <div>
          <ol class="ol">
            <li v-for="(todo, index) in todosNotDone" :key="todo" class="list">
              <div class="justifycontent flex2">
                <label class="checkbox">
                  <input type="checkbox" v-model="todo.done" />
                </label>
                <input
                  class="inputEdit"
                  type="text"
                  v-model="todo.text"
                  v-if="todo.edit"
                  @keyup.enter="toggleTodo(todo)"
                />
                <div
                  v-if="!todo.edit"
                  class="truncate"
                  :class="{ riscar: todo.done }"
                >
                  {{ todo.text }}
                </div>
                <input
                  type="button"
                  :value="todo.edit ? 'Salvar' : 'Editar'"
                  @click="toggleTodo(todo)"
                  class="buttonEdit"
                />

                <input
                  class="buttonRmv"
                  type="button"
                  value="X"
                  @click="removeTodo(index)"
                />
              </div>
            </li>
          </ol>
          <h4 class="listavazia" v-if="todos.length === 0">Lista vazia</h4>

          <h22 class="todolist2">Finalizados</h22>
          <ol class="ol">
            <li v-for="(todo, index) in todosDone" :key="todo" class="list">
              <div class="justifycontent flex2">
                <label class="checkbox">
                  <input type="checkbox" v-model="todo.done" />
                </label>
                <div class="truncate" :class="{ riscar: todo.done }">
                  {{ todo.text }}
                </div>
                <input
                  class="buttonRmv"
                  type="button"
                  value="X"
                  @click="removeTodo(index)"
                />
              </div>
            </li>
          </ol>
        </div>
        <h4 class="listavazia" v-if="todos.length === 0">Lista vazia</h4>
      </div>
    </div>
  </html>
</template>

<script>
export default {
  data() {
    return {
      edit: false,
      done: false,
      newTodo: "",
      todos: [],
    };
  },

  computed: {
    todosDone() {
      return this.todos.filter((a) => a.done);
    },
    todosNotDone() {
      return this.todos.filter((a) => !a.done);
    },
  },

  methods: {
    toggleTodo(todo) {
      todo.edit = !todo.edit;
    },
    addTodo() {
      if (this.newTodo !== "") {
        this.todos.push({ text: this.newTodo, done: false, edit: false });
        this.done = false;
        this.newTodo = "";
      }
    },

    remove() {
      this.todos = [];
    },

    removeTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style>
.borda {
  border-bottom: solid;
  border-color: rgb(143, 143, 143);
}
.listavazia {
  text-align: center;
  font: 16px arial;
  color: #666;
  padding-top: 20px;
}

.justifycontent {
  justify-content: space-between;
}

li {
  list-style-type: none;
}
.ol {
  padding-left: 0px;
}
.list {
  font: 18px arial;
  padding-bottom: 20px;
  border: 2px solid;
  border-radius: 5px;
  border-style: solid;
  border-color: rgb(143, 143, 143);
  padding: 15px;
  margin-bottom: 10px;
}
body {
  background-color: #040c3b;
  color: white;
}
.flex {
  display: flex;
}
.flex2 {
  display: flex;
  align-items: center;
}
.widht35 {
  width: 38%;
}
.todoApp {
  text-align: center;
  font: 50px arial;
  font-weight: bold;
}
.todolist {
  font: 30px arial;
  font-weight: bold;
  padding-right: 120px;
}
.todolist2 {
  font: 20px arial;
  font-weight: bold;
  padding-right: 120px;
}
.novotodo {
  font: 15px arial;
  font-weight: bold;
}
.truncate {
  width: 250px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.riscar {
  -webkit-text-decoration-line: line-through; /* Safari */
  text-decoration-line: line-through;
}

.input {
  background-color: transparent;
  width: 96%;
  border-style: solid;
  border-radius: 5px;
  border-color: rgb(143, 143, 143);
  color: white;
  font-size: 20px;
  padding: 5px;
  margin-bottom: 10px;
}
.inputEdit {
  background-color: transparent;
  width: 60%;
  border-style: solid;
  border-radius: 5px;
  border-color: rgb(143, 143, 143);
  color: white;
  font-size: 16px;
  padding: 5px;
}

.buttonRmv {
  border-radius: 5px;
  border-color: #a0a4d9;
  background-color: #a0a4d9;
  cursor: pointer;
  font-weight: bold;
  transition-duration: 0.3s;
}

.buttonRmv:hover {
  border-color: #9b0909;
  background-color: #f30b0b;
  color: white;
}

.buttonEdit {
  border-radius: 5px;
  border-color: #a0a4d9;
  background-color: #a0a4d9;
  cursor: pointer;
  font-weight: bold;
  transition-duration: 0.3s;
}

.buttonEdit:hover {
  background-color: #27292d;
  color: white;
}

.buttonEdit:active {
  background-color: #27292d;
  box-shadow: 0 2px #666;
  transform: translateY(4px);
}

.buttonAdd {
  font-weight: bold;
  height: 40px;
  padding-left: 155px;
  padding-right: 155px;
  border-radius: 6px;
  font-size: 18px;
  margin-bottom: 50px;
  background-color: #a0a4d9;
  border-style: solid;
  cursor: pointer;
  transition-duration: 0.3s;
}

.buttonAdd:hover {
  background-color: #27292d;
  color: white;
}
.buttonAdd:active {
  background-color: #27292d;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}

.buttonRemove {
  font-weight: bold;
  height: 30px;
  padding-left: 15px;
  padding-right: 15px;
  border-radius: 6px;
  font-size: 15px;
  margin-top: 0px;
  background-color: #a0a4d9;
  border-style: solid;
  cursor: pointer;
  transition-duration: 0.3s;
}

.buttonRemove:hover {
  background-color: #27292d;
  color: white;
}

.buttonRemove:active {
  background-color: #27292d;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}
</style>

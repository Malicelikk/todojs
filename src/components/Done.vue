<template>
  <div class="back">
    <div class="row" style="display:flex">
      <h3 style="display:inline-block">
        Done
        <span class="itemcount">{{itemcount}}</span>
        <span
          @click="gizlegoster()"
          style="display:inline-block;margin-left:auto;background-color:#D2DEFB;border-radius: 100px;padding: 5px;cursor:pointer"
        >+</span>
      </h3>
    </div>

    <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item"
    draggable="true" @dragstart="dragStart(index, $event)" @dragover.prevent @dragenter="dragEnter"
    @dragleave="dragLeave" @dragend="dragEnd" @drop="dragFinish(index, $event)">
      <div class="todo-item-left">
        <div v-if="!todo.editing" @dblclick="editTodo(todo)" class="todo-item-label">{{todo.title}}</div>
        <input
          v-else
          class="todo-item-edit"
          type="text"
          v-model="todo.title"
          @blur="doneEdit(todo)"
          @keyup.enter="doneEdit(todo)"
          @keyup.esc="cancelEdit(todo)"
        />
      </div>
      <div class="remove-item" @click="editTodo(todo)">Edit</div>
      <div class="remove-item" @click="removeTodo(index)">&times;</div>
    </div>

    <div v-if="goster" class="yenitask">
      <input
        type="text"
        class="todo-input"
        placeholder="New Task"
        v-model="newTodo"
        @keyup.enter="addTodo"
      />

    <div class="row">
        <img class="avatar" src="https://i.pravatar.cc/300" alt="">
        <p style="display:inline-block;font-weight: bolder;font-size: 15px;">Michael Russell</p>
        <button @click="addTodo" class="buton" style="display:inline-block;background-color:#D2DEFB;">Add</button>
        <button @click="gizlegoster()" class="buton" style="display:inline-block;background-color:white;">Cancel</button>

    </div>


    </div>

  </div>
</template>

<script>
export default {
  name: "todo-list",
  data() {
    return {
      newTodo: "",
      idForTodo: 3,
      beforeEditCache: "",
      dragging: -1,
      goster: false,
      todos: [
        {
          id: 1,
          title: "Design Landing Page For Support Team",
          completed: false,
          editing: false
        },
        {
          id: 2,
          title: "Design Landing Page For Support Team 2",
          completed: false,
          editing: false
        }
      ]
    };
  },
  computed: {
    itemcount() {
      return this.todos.length;
    },
     isDragging() {
      return this.dragging > -1
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length == 0) {
        return;
      }
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false
      });

      this.newTodo = "";
      this.idForTodo++;
      this.goster = false;
    },
    editTodo(todo) {
      this.beforeEditCache = todo.title;
      todo.editing = true;
    },
    doneEdit(todo) {
      if (todo.title.trim() == "") {
        todo.title = this.beforeEditCache;
      }
      todo.editing = false;
    },
    cancelEdit(todo) {
      todo.title = this.beforeEditCache;
      todo.editing = false;
    },
    gizlegoster() {
      this.goster = !this.goster;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
     dragStart(which, ev) {
      ev.dataTransfer.setData('Text', this.id);
      ev.dataTransfer.dropEffect = 'move'
      this.dragging = which;
    },
    dragEnter(ev) {
    },
    dragLeave(ev) {
    },
    dragEnd(ev) {
      this.dragging = -1
    },
    dragFinish(to, ev) {
      this.moveItem(this.dragging, to);
      ev.target.style.marginTop = '2px'
      ev.target.style.marginBottom = '2px'
    },
    moveItem(from, to) {
      if (to === -1) {
        this.removeItemAt(from);
      } else {
        this.todos.splice(to, 0, this.todos.splice(from, 1)[0]);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.avatar{
    vertical-align: middle;
    border-radius: 20px;
    width: 8%;
}

::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: #D2DEFB;
  opacity: 1; /* Firefox */
  font-size: 14px
}

.todo-input {
  border-radius: 20px;
  width: 100%;
  padding: 10px 18px;
  font-size: 18px;
  background-color: #FAFBFF;
  border-color: #D2DEFB
}

.todo-item {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: white;
  border-radius: 20px;
}

.remove-item {
  cursor: pointer;
  margin-right: 10px;
}

.todo-item-left {
  display: flex;
  align-items: center;
}
.todo-item-label {
  padding: 10px;
  border: 1px solid white;
  margin-left: 12px;
  color: black;
  font-size: 18px;
}
.todo-item-edit {
  font-size: 24px;
  color: #2c3e50;
  margin-left: 12px;
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}

.back {
  background-color: #f2f6fa;
  padding: 10px;
  display: inline-block;
  width: 18%;
  border-radius: 20px;
  vertical-align: top;
}

.buton {     
        padding: 8px;
    border-radius: 10px;
    border-color: transparent;
    cursor: pointer;
}

.yenitask{
    padding: 10px;
    background-color: white;
    border-radius: 20px;
}
.itemcount{background-color:#D2DEFB;border-radius: 100px;padding: 5px;font-weight: 600;
    font-size: 16px;}
</style>

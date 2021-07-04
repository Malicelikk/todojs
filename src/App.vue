<template>
  <div id="app" class="container">
    <img src="./assets/logo.png" class="logo">
    <h2 style="color:black">Kanban Board</h2>
    <todo-list/>
    <InProgress/>
    <Test/>
    <Done/>
    <AddNew/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import TodoList from './components/TodoList'
import InProgress from './components/InProgress'
import Test from './components/Test'
import Done from './components/Done'
import AddNew from './components/AddNew'


export default {
  name: 'App',
  components: {
    HelloWorld,
    TodoList,
    InProgress,
    Test,
    Done,
    AddNew
  }
}
</script>

<style>

* {
  box-sizing: border-box
}

.container { max-width: 95%;
      margin: 0 auto;
}


#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  margin-top: 60px;
  font-size: 20px;
}

.logo{display: block;
margin: 20px auto;
height: 75px;}

</style>

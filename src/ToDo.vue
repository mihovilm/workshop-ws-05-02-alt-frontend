<template>
  <div id="app">
    <div class="ToDo">
    <img class="Logo" :src="logo" alt="Vue logo"/>
    <h1 class="ToDo-Header"> Vue Workshop</h1>
      <div class="ToDo-Container">
        <div class="ToDo-Content">  
          <ToDoItem  
            v-for="todo in list"
            :todo="todo"
            @delete="onDeleteItem"
            :key="todo.id"  />

            <tinymce id="d1"
                      :other_options="tinyOptions"
                      v-model="todo"
                      v-on:keyup.enter="createNewToDoItem"
            ></tinymce>
<div  class="ToDo-Add"  @click="createNewToDoItem()">+</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from './assets/logo.png'
import ToDoItem from './components/ToDoItem.vue'
import tinymce from 'vue-tinymce-editor';


export default {
  name:  'to-do',
  components: {
    ToDoItem,
    tinymce,
  },
  data() {
     return {
            list: [
                {
                  id: 1,
                  text: 'Stretch Break'
                },
                {
                  id: 2,
                  text: 'Wait 15 minutes'
                },
                {
                  id: 3,
                  text: 'Stretch Break(again)'
                }
            ],
            todo: '',
            logo: Logo,
            tinyOptions: {
                      'height': 200
              },
        }
    },
    methods: {
      createNewToDoItem() {
      //Make sure something is in todo
        if (!this.todo){
          alert("You need to enter some text!");
          return
        }

        const newId = Math.max.apply(null, this.list.map(t  =>  t.id)) + 1;

        this.list.push({ id:  newId, text:  this.todo });

        this.todo = '';

      },
      onDeleteItem(todo){

        this.list = this.list.filter(item  =>  item !== todo);

      }

    }
}
</script>

<style>
  body {
    margin: 0;
    padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica, Arial, sans-serif;
    background: linear-gradient(#aeffae, #3d99ff);
    height: auto;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .Logo {
    width: 50px;
    position: relative;
    top: 50px;
  }

  .ToDo {
    text-align: center;
    border: 1px solid white;
    width: 80vw;
    height: auto;
    box-shadow: 2px 3px 15px rgba(0, 0, 0, 0.5);
    background: #f6f6f6;
    padding-bottom: 60px;
    margin: 40px auto;
  }

  .ToDo-Header {
    color: black;
    font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica, Arial, sans-serif;
    font-weight: 400;
    text-transform: uppercase;
    margin: 70px auto 30px;
  }

  .ToDo-Add {
    color: white;
    font-size: 2em;
    width: 0.5em;
    height: 0.5em;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 15px;
    cursor: pointer;
    background: #73ff73;
    border-radius: 10px;
    box-shadow: 1px 1px 1px #47a947;
    margin: 20px auto 0;
  }

  .ToDo-Add:hover {
    box-shadow: none;
    margin-top: 21px;
    margin-left: calc(auto + 1px);
  }

  .ToDo-Container {
    width: 80%;
    margin: 0 auto;
  }

  input {
    width: 60%;
    padding: 10px;
    font-size: 1em;
    margin: 10px auto;
    box-shadow: 1px 3px 20px 0px rgba(0, 0, 0, 0.3)
  }
</style>
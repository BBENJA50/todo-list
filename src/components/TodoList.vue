<script setup>

import {useTodoListStore} from "@/stores/todoList.js";
import {storeToRefs} from "pinia";

const store = useTodoListStore()
const {todoList} = storeToRefs(store) //Hier slaan we alle lijstitems op in de todoList constante als reactive
const {toggleCompleted, deleteTodo} = store
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col-md-4 offset-md-4">
        <ul v-for="todo in todoList" :key="todo.id" class="list-group mb-1">
          <li class="list-group-item d-flex justify-content-between  bg-secondary-subtle" :class="{completed:todo.completed}">
            <span >{{todo.id +1}} - {{todo.item}}</span>
            <div>
              <span @click.stop="toggleCompleted(todo.id)" class="pointer border border-black p-1 me-1">&#10004;</span>
              <span @click="deleteTodo(todo.id)" class="pointer border border-black p-1">&#10060;</span>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>

</template>

<style scoped>
.completed{
  text-decoration: line-through;
}
.pointer:hover{
  cursor: pointer;
  user-select: none;
  background-color: darkcyan;
}
</style>

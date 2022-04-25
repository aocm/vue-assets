<script setup lang="ts">
import { storeToRefs } from 'pinia'
import { reactive } from 'vue'
import { useTodoStore } from '../store/todos'

const state = reactive({ newTodoLabel: '' })

// useTodoStore を呼び出すだけで、グローバルストアへのアクセスが可能
const store = useTodoStore()

// ストア内の State や Getters はリアクティブオブジェクトなので、
// リアクティブを失わずに取り出す場合は storeToRefs を用いる
const { filteredTodos, filter } = storeToRefs(store)

const toggleTodo = (id: number) => store.toggleTodo(id)
const addTodo = () => {
  if (state.newTodoLabel !== '') {
    store.addTodo(state.newTodoLabel)
    state.newTodoLabel = ''
  }
}
</script>

<template>
  <input v-model="state.newTodoLabel" />
  <button @click="addTodo">add</button>

  <input id="all" v-model="filter" type="radio" value="all" />
  <label for="all">すべて</label>
  <input id="finished" v-model="filter" type="radio" value="finished" />
  <label for="finished">完了済み</label>
  <input id="unfinished" v-model="filter" type="radio" value="unfinished" />
  <label for="unfinished">未完了</label>

  <ul>
    <li
      v-for="todo in filteredTodos"
      :key="todo.label"
      :class="{ todo: true, finished: todo.finished }"
      @click="toggleTodo(todo.id)"
      v-text="todo.label"
    />
  </ul>
</template>

<style scoped>
.todo {
  user-select: none;
  cursor: pointer;
}
.todo.finished {
  text-decoration: line-through;
  color: gray;
}
</style>

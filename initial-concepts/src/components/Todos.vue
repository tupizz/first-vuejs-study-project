<template>
  <div>
    <h1>Todo Modules</h1>

    <ul>
      <li v-for="todo in notDoneTodos" :key="todo.text">
        {{ todo.text }}
        <button class="done-todo" @click="doneIt(todo)">finalizar ✅</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

interface Todo {
  text: string
  done: boolean
}

export default defineComponent({
  data() {
    return {
      todos: [] as Todo[]
    }
  },
  setup() {
    return {}
  },
  methods: {
    doneIt(t: Todo) {
      const todosCopy: Todo[] = [...this.todos]

      const todoItem = todosCopy.find((todo) => todo.text === t.text)
      todoItem!.done = true

      this.todos = todosCopy
    }
  },
  created() {
    this.todos = [
      { text: 'Estudar Typescript', done: true },
      { text: 'Lavar os pratos', done: false },
      { text: 'Ler um livro', done: false },
      { text: 'Aprender Nuxt.js', done: true }
    ]
  },
  watch: {
    todos(newValue: Todo[]) {
      const isFinished = !newValue.some((todo) => !todo.done)
      if (isFinished) {
        alert('Done with all!')
      }
    }
  },
  computed: {
    notDoneTodos(): Todo[] {
      return this.todos.filter((todo) => !todo.done)
    }
  }
})
</script>

<style scoped>
div {
  background-color: #fafafa;
  font-family: 'Courier New', Courier, monospace;
}

ul li {
  margin-top: 5px;
}

.done-todo {
  background: none;
  border: 1px solid #babaca;
  border-radius: 5px;
  cursor: pointer;
  color: green;
}
</style>

<template>
  <div>
    <h1>Todo Modules</h1>

    <a href="#intern" v-on:click="something">intern link 1</a>
    <a href="#intern" v-on:click.prevent="something">intern link 2 </a>
    <a href="#intern" v-on:click.once="something">intern link 3</a>
    <a href="#intern" v-on:click.once.prevent="something">intern link 4</a>

    <!-- insted of using 'v-on:' we can use just '@'  -->
    <a href="#intern" @click.once.prevent="something">intern link 4</a>

    <!-- Event handling // Event modifiers  -->
    <!-- Whenever I press "enter" this will fire up -->
    <input type="text" @keyup.enter="keyupEventEnter" />

    <ul>
      <li v-for="todo in notDoneTodos" :key="todo.text">
        <!-- <a
          v-bind:class="todo.done ? 'done' : 'not-done'"
          v-bind:href="todo.href"
          >{{ todo.text }}</a
        > -->
        <!-- The directive v-bind has a shortcut that is ":" -->
        <a :class="todo.done ? 'done' : 'not-done'" :href="todo.href">{{
          todo.text
        }}</a>
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
  href: string
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
    },
    something() {
      console.log('was clicked! 😅')
    },
    keyupEventEnter() {
      console.log('keyup')
    }
  },
  created() {
    this.todos = [
      {
        text: 'Estudar Typescript',
        href: 'www.amazon.com/product1',
        done: true
      },
      {
        text: 'Lavar os pratos',
        href: 'https://www.amazon.com/product1',
        done: false
      },
      {
        text: 'Ler um livro',
        href: 'https://www.amazon.com/product1',
        done: false
      },
      {
        text: 'Aprender Nuxt.js',
        href: 'https://www.amazon.com/product1',
        done: true
      }
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

.not-done {
  color: darkred;
}

.done-todo {
  background: none;
  border: 1px solid #babaca;
  border-radius: 5px;
  cursor: pointer;
  color: green;
}
</style>

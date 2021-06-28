<template>
  <div>
    <!-- Header importando -->
    <Header />

    <ButtonStyled text="teste" />

    <!-- Linha -->
    <hr />

    <h1>Contador: {{ count }}</h1>
    <button @click="increment">Incrementar</button>
    <button @click="decrement">Decrementar</button>
    <button @click="reset">Resetar</button>

    <!-- Linha -->
    <hr />

    <!-- Computed property -->
    <h1>Nome: {{ fullName }}</h1>

    <!-- Linha -->
    <hr />

    <!-- Todo moduel -->
    <Todos />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Header from '@/components/Header.vue'
import Todos from '@/components/Todos.vue'
import ButtonStyled from '@/components/ButtonStyled.vue'

export default defineComponent({
  // data props exposed to template
  data() {
    return {
      name: 'tadeu',
      lastName: 'tupinamba',
      count: 0
    }
  },

  // methos exposed to template
  methods: {
    increment() {
      this.count++
    },
    decrement() {
      if (this.count === 0) return
      this.count--
    },
    reset() {
      this.count = 0
    }
  },

  // hooks
  beforeCreate() {
    console.log('triggered before creation')
  },
  // here we can acess the data objects
  created() {
    console.log('tiggered after creation')
  },
  beforeMount() {
    console.log('tiggered before dom mount')
  },
  // here we can acess the dom
  mounted() {
    console.log(this.$el)
  },
  updated() {
    console.log('updated state')
  },

  // importing components that we will use
  components: {
    Header,
    Todos,
    ButtonStyled
  },

  // wathcing data objects
  watch: {
    count(newvalue, oldvalue) {
      console.log(`Novo valor: ${newvalue} // Valor Antigo: ${oldvalue}`)
    }
  },

  // defining computed props
  computed: {
    fullName(): string {
      return `${this.name} ${this.lastName}`
    }
  }
})
</script>

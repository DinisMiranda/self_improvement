# Vue.js — referência rápida

*CLI, componentes com Options API, Router e Pinia. Para consulta enquanto trabalhas.*

---

## Criar e correr projeto

```bash
# criar projeto (Vue 3)
npm create vue@latest nome-do-projeto

# dentro do projeto
npm install
npm run dev
```

- **Build:** `npm run build`  
- **Testes:** `npm run test` (conforme config do template)  
- **Lint:** `npm run lint`

---

## Estrutura de um componente (Options API)

```vue
<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  computed: {
    doubled() {
      return this.count * 2
    }
  },
  methods: {
    increment() {
      this.count++
    }
  },
  mounted() {
    console.log('montado')
  }
}
</script>

<template>
  <button @click="increment">{{ count }} ({{ doubled }})</button>
</template>
```

- **data()** — devolve o objeto reativo do componente; aceder com `this.count`.
- **computed** — propriedades derivadas; atualizam quando as dependências mudam.
- **methods** — funções; usar `this.nomeDoMetodo` no template ou noutros métodos.
- **mounted()** — corre depois de o componente ser montado no DOM.

---

## Diretivas comuns

| Diretiva | Uso |
|----------|-----|
| **`v-model`** | Two-way binding: `v-model="text"` (input, textarea, select) |
| **`v-if`** / **`v-else-if`** / **`v-else`** | Mostrar/ocultar (remove do DOM) |
| **`v-show`** | Mostrar/ocultar com CSS (display) |
| **`v-for`** | Loop: `v-for="item in list" :key="item.id"` — **sempre** usar `:key` estável |
| **`v-bind`** ou **`:`** | Atributo: `:href="url"` |
| **`v-on`** ou **`@`** | Evento: `@click="handleClick"` |
| **`v-slot`** ou **`#`** | Slots (conteúdo passado pelo pai) |

---

## Props e eventos

```vue
<!-- Filho -->
<script>
export default {
  props: {
    title: String,
    count: { type: Number, default: 0 }
  },
  methods: {
    notifyParent() {
      this.$emit('update', this.count)
      this.$emit('close')
    }
  }
}
</script>

<!-- Pai -->
<Child :title="name" @update="onUpdate" @close="onClose" />
```

- **props** — definição das propriedades que o componente recebe; só leitura.
- **this.$emit('nomeEvento', valor)** — emite um evento para o pai.

---

## Vue Router

```javascript
// router/index.js
import { createRouter, createWebHistory } from 'vue-router'
const routes = [
  { path: '/', component: Home },
  { path: '/user/:id', component: User, name: 'user' }
]
const router = createRouter({ history: createWebHistory(), routes })
```

Num componente (Options API):
- **`<router-link to="/">Home</router-link>`** ou **`to="{ name: 'user', params: { id: 1 } }"`**
- **`<router-view />`** — onde aparece o componente da rota
- **`this.$router`** — `this.$router.push('/path')`, `this.$router.replace()`, etc.
- **`this.$route`** — `this.$route.params`, `this.$route.query`

---

## Pinia (estado global)

```javascript
// stores/counter.js
import { defineStore } from 'pinia'
export const useCounterStore = defineStore('counter', {
  state: () => ({ count: 0 }),
  getters: {
    doubled: (state) => state.count * 2
  },
  actions: {
    increment() {
      this.count++
    }
  }
})
```

Num componente (Options API) — usar a store em `created` ou `mounted` e guardar em `data`:

```vue
<script>
import { useCounterStore } from '@/stores/counter'

export default {
  data() {
    return {
      store: null
    }
  },
  created() {
    this.store = useCounterStore()
  },
  methods: {
    increment() {
      this.store.increment()
    }
  }
}
</script>

<template>
  <div>{{ store?.count }} — {{ store?.doubled }}</div>
  <button @click="increment">+</button>
</template>
```

Ou com **mapState** / **mapActions** (helpers do Pinia para Options API):

```javascript
import { mapState, mapActions } from 'pinia'
import { useCounterStore } from '@/stores/counter'

export default {
  computed: {
    ...mapState(useCounterStore, ['count', 'doubled'])
  },
  methods: {
    ...mapActions(useCounterStore, ['increment'])
  }
}
```

---

## Lifecycle (Options API)

| Hook | Quando corre |
|------|----------------|
| **beforeCreate** | Antes de criar a instância |
| **created** | Depois de criar (data, computed disponíveis; ainda sem DOM) |
| **beforeMount** | Antes de montar no DOM |
| **mounted** | Depois de montar no DOM |
| **beforeUpdate** | Antes de re-renderizar (dados mudaram) |
| **updated** | Depois de o DOM ser atualizado |
| **beforeUnmount** | Antes de desmontar (Vue 3) |
| **unmounted** | Depois de desmontar |

*(Em Vue 2 os últimos dois chamam-se beforeDestroy e destroyed.)*

---

## Dicas rápidas

- **`v-if` vs `v-show`:** `v-if` não renderiza; `v-show` esconde com CSS. Para alternar frequentemente, `v-show` pode ser melhor.
- **Keys em `v-for`:** usar um id estável (nunca o índice se a lista mudar com reordenação/inserção).
- **Reutilizar lógica (Options API):** mixins ou colocar lógica na store (Pinia). Em Vue 3 o Pinia substitui bem a Vuex.
- **Teleport:** `<Teleport to="body">` para renderizar conteúdo noutro sítio do DOM (modais, toasts).

*Podes acrescentar aqui snippets teus, convenções de pastas e comandos dos teus projetos Vue.*

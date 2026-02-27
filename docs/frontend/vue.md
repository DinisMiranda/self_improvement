# Vue.js — quick reference

*CLI, components with Options API, Router, and Pinia. For lookup while you work.*

---

## Create and run project

```bash
# create project (Vue 3)
npm create vue@latest project-name

# inside the project
npm install
npm run dev
```

- **Build:** `npm run build`  
- **Test:** `npm run test` (depends on template config)  
- **Lint:** `npm run lint`

---

## Component structure (Options API)

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
    console.log('mounted')
  }
}
</script>

<template>
  <button @click="increment">{{ count }} ({{ doubled }})</button>
</template>
```

- **data()** — returns the component's reactive object; access with `this.count`.
- **computed** — derived properties; update when dependencies change.
- **methods** — functions; use `this.methodName` in template or other methods.
- **mounted()** — runs after the component is mounted in the DOM.

---

## Common directives

| Directive | Use |
|-----------|-----|
| **`v-model`** | Two-way binding: `v-model="text"` (input, textarea, select) |
| **`v-if`** / **`v-else-if`** / **`v-else`** | Show/hide (removes from DOM) |
| **`v-show`** | Show/hide with CSS (display) |
| **`v-for`** | Loop: `v-for="item in list" :key="item.id"` — **always** use a stable `:key` |
| **`v-bind`** or **`:`** | Attribute: `:href="url"` |
| **`v-on`** or **`@`** | Event: `@click="handleClick"` |
| **`v-slot`** or **`#`** | Slots (content passed from parent) |

---

## Props and events

```vue
<!-- Child -->
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

<!-- Parent -->
<Child :title="name" @update="onUpdate" @close="onClose" />
```

- **props** — definition of properties the component receives; read-only.
- **this.$emit('eventName', value)** — emit an event to the parent.

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

In a component (Options API):
- **`<router-link to="/">Home</router-link>`** or **`to="{ name: 'user', params: { id: 1 } }"`**
- **`<router-view />`** — where the route component is rendered
- **`this.$router`** — `this.$router.push('/path')`, `this.$router.replace()`, etc.
- **`this.$route`** — `this.$route.params`, `this.$route.query`

---

## Pinia (global state)

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

In a component (Options API) — use the store in `created` or `mounted` and store it in `data`:

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

Or with **mapState** / **mapActions** (Pinia helpers for Options API):

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

| Hook | When it runs |
|------|----------------|
| **beforeCreate** | Before the instance is created |
| **created** | After creation (data, computed available; no DOM yet) |
| **beforeMount** | Before mounting to DOM |
| **mounted** | After mounted to DOM |
| **beforeUpdate** | Before re-render (data changed) |
| **updated** | After DOM is updated |
| **beforeUnmount** | Before unmounting (Vue 3) |
| **unmounted** | After unmounted |

*(In Vue 2 the last two are called beforeDestroy and destroyed.)*

---

## Quick tips

- **`v-if` vs `v-show`:** `v-if` doesn't render; `v-show` hides with CSS. For toggling often, `v-show` may be better.
- **Keys in `v-for`:** use a stable id (never the index if the list can be reordered or items inserted).
- **Reusing logic (Options API):** mixins or put logic in the store (Pinia). In Vue 3 Pinia replaces Vuex well.
- **Teleport:** `<Teleport to="body">` to render content elsewhere in the DOM (modals, toasts).

*You can add your own snippets, folder conventions, and commands from your Vue projects here.*

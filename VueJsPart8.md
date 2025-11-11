# 🚀 Cours 8 — Projet final : mini app complète

---

## 🎯 Objectif du projet

Ce projet a pour but de **mettre en pratique tout ce que tu as appris avec Vue.js** à travers la création d’une petite application complète.

Tu vas :  
✅ Créer une app Vue avec un vrai composant racine et plusieurs sous-composants  
✅ Gérer les données via Pinia  
✅ Utiliser les événements et propriétés (`props` / `emit`)  
✅ Intégrer une API simple  
✅ Ajouter un peu de style et des transitions

---

## 🧱 Structure du projet

```
projet-final-vue/
│
├── src/
│   ├── components/
│   │   ├── TodoItem.vue
│   │   └── TodoForm.vue
│   ├── store/
│   │   └── todoStore.js
│   ├── App.vue
│   └── main.js
│
├── index.html
└── package.json
```

---

## 1️⃣ Création du projet

Crée un projet avec **Vite** :

```bash
npm create vite@latest projet-final-vue
cd projet-final-vue
npm install
npm run dev
```

Installe **Vue** et **Pinia** :

```bash
npm install vue pinia
```

---

## 2️⃣ App.vue — le composant principal

```vue
<template>
  <div class="container">
    <h1>📝 Ma Todo App Vue.js</h1>
    <TodoForm />
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggle="toggleTodo(todo.id)"
      @delete="deleteTodo(todo.id)"
    />
  </div>
</template>

<script setup>
import { useTodoStore } from './store/todoStore'
import TodoForm from './components/TodoForm.vue'
import TodoItem from './components/TodoItem.vue'

const store = useTodoStore()
const todos = store.todos
const toggleTodo = store.toggleTodo
const deleteTodo = store.deleteTodo
</script>
```

---

## 3️⃣ Store Pinia : `todoStore.js`

```js
import { defineStore } from 'pinia'

export const useTodoStore = defineStore('todo', {
  state: () => ({
    todos: [
      { id: 1, text: 'Découvrir Vue.js', done: false },
      { id: 2, text: 'Apprendre Pinia', done: false }
    ]
  }),
  actions: {
    addTodo(text) {
      this.todos.push({ id: Date.now(), text, done: false })
    },
    toggleTodo(id) {
      const todo = this.todos.find(t => t.id === id)
      todo.done = !todo.done
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    }
  }
})
```

---

## 4️⃣ Composant `TodoForm.vue`

```vue
<template>
  <form @submit.prevent="add">
    <input v-model="text" placeholder="Nouvelle tâche..." />
    <button>Ajouter</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'
import { useTodoStore } from '../store/todoStore'

const text = ref('')
const store = useTodoStore()

const add = () => {
  if (text.value.trim()) {
    store.addTodo(text.value)
    text.value = ''
  }
}
</script>
```

---

## 5️⃣ Composant `TodoItem.vue`

```vue
<template>
  <div class="todo-item">
    <input type="checkbox" :checked="todo.done" @change="$emit('toggle')" />
    <span :class="{ done: todo.done }">{{ todo.text }}</span>
    <button @click="$emit('delete')">❌</button>
  </div>
</template>

<script setup>
defineProps(['todo'])
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 8px;
}
.done {
  text-decoration: line-through;
  color: gray;
}
</style>
```

---

## 6️⃣ Améliorations possibles

- Ajouter une **API** pour sauvegarder les tâches (ex : JSONPlaceholder ou ton backend Laravel)  
- Ajouter un **filtre** (toutes / terminées / actives)  
- Gérer des **catégories de tâches**
- Ajouter des **animations** sur l’ajout / suppression (transition Vue)

---

## 🧩 Conclusion

Tu as maintenant une **application Vue.js complète**, utilisant les composants, les événements, Pinia, et un peu de style 🎨  
C’est une excellente base avant de te lancer sur un vrai projet pro ou de passer à **Vue Router** 🚀

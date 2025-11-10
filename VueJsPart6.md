# 🧠 Cours 6 — La gestion d’état avec Pinia 🏪

---

## 🎯 Objectifs du cours
À la fin de ce cours, tu sauras :

✅ Comprendre ce qu’est un **store global**  
✅ Utiliser **Pinia** pour partager des données entre composants  
✅ Créer, modifier et lire l’état global  
✅ Organiser ton code de manière claire et scalable  

---

## 🧩 1. Pourquoi utiliser un store ?

Dans une application Vue, les composants ont chacun leur état (`data`).  
Mais parfois, plusieurs composants ont besoin de **partager des données communes** (ex : l’utilisateur connecté, le panier, les paramètres du thème…).

> 📦 Un **store** est une zone centrale où tu stockes ces données pour les rendre accessibles partout.

---

## ⚙️ 2. Installation de Pinia

Pinia est le **gestionnaire d’état officiel** pour Vue.js (successeur de Vuex).

Installe-le dans ton projet :

```bash
npm install pinia
```

Puis ajoute-le à ton app :

```js
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'

const app = createApp(App)
app.use(createPinia())
app.mount('#app')
```

---

## 🧱 3. Créer ton premier store

Crée un dossier `stores/` à la racine de `src/`, puis un fichier `useUserStore.js` :

```js
import { defineStore } from 'pinia'

export const useUserStore = defineStore('user', {
  state: () => ({
    name: 'Nico',
    isLoggedIn: false
  }),
  actions: {
    login(name) {
      this.name = name
      this.isLoggedIn = true
    },
    logout() {
      this.name = ''
      this.isLoggedIn = false
    }
  }
})
```

---

## 🧩 4. Utiliser le store dans un composant

Tu peux maintenant **importer et utiliser** ton store dans n’importe quel composant :

```vue
<script setup>
import { useUserStore } from '@/stores/useUserStore'
const userStore = useUserStore()

function seConnecter() {
  userStore.login('Nico')
}
</script>

<template>
  <div>
    <p v-if="userStore.isLoggedIn">
      Bonjour, {{ userStore.name }} !
      <button @click="userStore.logout">Se déconnecter</button>
    </p>
    <p v-else>
      <button @click="seConnecter">Se connecter</button>
    </p>
  </div>
</template>
```

---

## 🧠 5. Computed & Getters

Les **getters** sont comme des propriétés calculées globales :

```js
export const usePanierStore = defineStore('panier', {
  state: () => ({
    produits: []
  }),
  getters: {
    totalPrix: (state) => state.produits.reduce((acc, p) => acc + p.prix, 0)
  }
})
```

Puis dans ton composant :

```vue
<p>Total du panier : {{ panierStore.totalPrix }} €</p>
```

---

## 🧩 6. Bonus — Persistance du store

Tu peux conserver l’état de ton store après rechargement grâce à un plugin comme :

```bash
npm install pinia-plugin-persistedstate
```

Puis :

```js
import { createPinia } from 'pinia'
import piniaPersistedState from 'pinia-plugin-persistedstate'

const pinia = createPinia()
pinia.use(piniaPersistedState)
```

Et dans ton store :

```js
export const useUserStore = defineStore('user', {
  state: () => ({
    name: '',
    isLoggedIn: false
  }),
  persist: true
})
```

---

## 🏁 Conclusion

Tu sais maintenant comment :

✅ Créer un **store Pinia**  
✅ Gérer des **données globales** partagées  
✅ Manipuler ces données via des **actions et getters**  
✅ Rendre l’état **persistant** pour une meilleure expérience utilisateur

> 🔥 Pinia est essentiel pour toute app Vue.js un peu complexe — il rend la gestion d’état simple et puissante.

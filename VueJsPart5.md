# 🧠 Cours 5 — Le routage avec Vue Router 🧭

---

## 🎯 Objectifs du cours

À la fin de ce cours, tu sauras :

✅ Comprendre le rôle du **routage** dans une application Vue.js  
✅ Configurer **Vue Router** dans un projet  
✅ Créer des **routes dynamiques** et utiliser les **paramètres d’URL**  
✅ Naviguer entre les pages avec `<router-link>` et `<router-view>`  
✅ Protéger certaines routes et gérer la redirection

---

## 🚀 1. Qu’est-ce que Vue Router ?

**Vue Router** est le système de navigation officiel de Vue.js.  
Il permet de créer une **application monopage (SPA)** où la navigation ne recharge pas la page entière.

> 🔍 En clair : chaque "page" de ton site devient un composant Vue, affiché selon l’URL.

---

## ⚙️ 2. Installation

Dans un projet Vue 3 (créé avec `npm init vue@latest`), installe Vue Router :

```bash
npm install vue-router
```

---

## 🧩 3. Configuration de base

Crée un fichier `router/index.js` :

```js
import { createRouter, createWebHistory } from 'vue-router'
import HomeView from '../views/HomeView.vue'
import AboutView from '../views/AboutView.vue'

const routes = [
  { path: '/', name: 'home', component: HomeView },
  { path: '/about', name: 'about', component: AboutView }
]

const router = createRouter({
  history: createWebHistory(),
  routes
})

export default router
```

Puis importe-le dans `main.js` :

```js
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

createApp(App).use(router).mount('#app')
```

---

## 🧭 4. Afficher les vues avec `<router-view>`

Dans ton `App.vue` :

```html
<template>
  <nav>
    <router-link to="/">Accueil</router-link> |
    <router-link to="/about">À propos</router-link>
  </nav>

  <router-view></router-view>
</template>
```

🪄 `<router-view>` est la zone où les composants correspondant aux routes s’affichent.

---

## 🧠 5. Routes dynamiques

Tu peux créer des routes avec des **paramètres** :

```js
{ path: '/user/:id', name: 'user', component: UserView }
```

Dans `UserView.vue` :

```html
<template>
  <h2>Profil de l’utilisateur {{ $route.params.id }}</h2>
</template>
```

🧩 URL : `/user/42` affichera “Profil de l’utilisateur 42”.

---

## 🔄 6. Redirections et routes 404

Tu peux rediriger ou gérer une route inexistante :

```js
{ path: '/home', redirect: '/' },
{ path: '/:pathMatch(.*)*', name: 'NotFound', component: NotFoundView }
```

---

## 🔒 7. Protéger une route (guard)

Tu peux intercepter la navigation avant de changer de page :

```js
router.beforeEach((to, from, next) => {
  const isAuthenticated = false // à remplacer par ta logique
  if (to.name === 'about' && !isAuthenticated) next({ name: 'home' })
  else next()
})
```

> 💡 Très utile pour bloquer l’accès à une page sans être connecté.

---

## 🧠 En résumé

| Élément | Rôle |
|----------|------|
| `createRouter()` | Crée le routeur |
| `<router-link>` | Permet la navigation interne |
| `<router-view>` | Zone d’affichage des composants de page |
| `:to` | Lien vers une route spécifique |
| `beforeEach()` | Vérifie / bloque la navigation avant de changer de page |

---

## 💪 Exercice pratique

Crée une mini app avec 3 pages :
- Accueil (texte simple)
- À propos (description)
- Profil utilisateur (route dynamique : `/user/:id`)

Ajoute une redirection de `/home` vers `/` et une page 404.

🎯 **Bonus :** bloque l’accès à la page "À propos" si l’utilisateur n’est pas connecté (variable booléenne).

---

🎓 **Prochain cours :** Les formulaires et la gestion des données utilisateur dans Vue.js 🧾

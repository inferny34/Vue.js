# 🧠 Cours 7 — Connexion à une API avec Vue.js 🌐

---

## 🎯 Objectifs du cours
À la fin de ce cours, tu sauras :

✅ Comprendre ce qu’est une API et comment l’utiliser avec Vue.js  
✅ Récupérer des données distantes avec `fetch` ou `axios`  
✅ Afficher ces données dans ton interface  
✅ Gérer les erreurs et les chargements  

---

## 🧩 1. Qu’est-ce qu’une API ?

Une **API (Application Programming Interface)** permet à ton application d’échanger des données avec un serveur distant.  
Par exemple : récupérer des utilisateurs, des produits, ou des articles depuis une base de données externe.

> 🌍 Exemple : `https://jsonplaceholder.typicode.com/users` retourne une liste d’utilisateurs de test.

---

## ⚙️ 2. Installation d’Axios (optionnel mais recommandé)

Vue.js peut utiliser `fetch` (natif) ou **axios** (librairie plus complète) pour appeler des API.

Installe Axios avec :

```bash
npm install axios
```

---

## 📡 3. Exemple avec Fetch

```vue
<script setup>
import { ref, onMounted } from 'vue'

const users = ref([])
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users')
    if (!response.ok) throw new Error('Erreur serveur')
    users.value = await response.json()
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
})
</script>

<template>
  <div>
    <p v-if="loading">Chargement...</p>
    <p v-if="error">❌ Erreur : {{ error }}</p>
    <ul v-if="!loading && !error">
      <li v-for="user in users" :key="user.id">
        👤 {{ user.name }} — {{ user.email }}
      </li>
    </ul>
  </div>
</template>
```

---

## ⚙️ 4. Exemple avec Axios

```vue
<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const posts = ref([])
const loading = ref(true)

onMounted(async () => {
  try {
    const res = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=5')
    posts.value = res.data
  } catch (e) {
    console.error('Erreur API:', e)
  } finally {
    loading.value = false
  }
})
</script>

<template>
  <div>
    <p v-if="loading">Chargement des articles...</p>
    <ul v-else>
      <li v-for="post in posts" :key="post.id">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
      </li>
    </ul>
  </div>
</template>
```

---

## 🧠 5. Bonus — Afficher un message d’attente

Tu peux améliorer l’expérience utilisateur avec un petit indicateur de chargement :

```vue
<p v-if="loading">⏳ Chargement...</p>
<p v-else-if="error">❌ Erreur : {{ error }}</p>
<p v-else>✅ Données chargées avec succès !</p>
```

---

## 💪 6. Exercice pratique

Crée une mini-app qui affiche des **photos** à partir de l’API suivante :  
👉 `https://jsonplaceholder.typicode.com/photos?_limit=10`

**Objectifs :**
- Afficher 10 images avec leur titre
- Ajouter un bouton "Recharger" pour rafraîchir la liste
- Gérer le chargement et les erreurs

---

## 🏁 Conclusion

Tu sais maintenant comment :
✅ Te connecter à une **API REST**  
✅ Charger et afficher des données externes  
✅ Gérer les états `loading`, `error`, et `success`  
✅ Utiliser `fetch` ou `axios` selon tes préférences  

> 🌐 Les appels API sont essentiels pour toute app moderne : c’est la clé pour connecter ton front-end à un back-end !

# 🧠 Cours 3 — Les composants Vue.js : créer, structurer et réutiliser

---

## 🎯 Objectifs du cours

À la fin de ce cours, tu sauras :

✅ Ce qu’est un **composant Vue**  
✅ Comment le créer et l’utiliser  
✅ Comment faire communiquer les composants entre eux (props & events)  
✅ Structurer une petite application modulaire avec plusieurs composants

---

## 🧩 1. Qu’est-ce qu’un composant ?

Un **composant** est une **brique réutilisable** d’interface utilisateur.

Chaque composant a :
- Son **HTML** (template)
- Son **JavaScript** (logique, data, méthodes)
- Son **CSS** (style optionnel)

> 🧱 En gros : un composant = un mini bout d’application autonome.

---

## 🧠 2. Créer son premier composant

### Exemple avec Vue 3 en CDN :

```html
<div id="app">
  <user-card></user-card>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
const app = Vue.createApp({})

app.component('user-card', {
  template: `
    <div class="card">
      <h2>{{ name }}</h2>
      <p>{{ role }}</p>
    </div>
  `,
  data() {
    return {
      name: "Nico",
      role: "Développeur Web"
    }
  }
})

app.mount('#app')
</script>
```

---

## 💬 3. Communication entre composants : les **props**

Les **props** permettent de **transmettre des données** du parent à l’enfant.

```html
<div id="app">
  <user-card name="Nico" role="Développeur Web"></user-card>
  <user-card name="Laurie" role="UI Designer"></user-card>
</div>

<script>
const app = Vue.createApp({})

app.component('user-card', {
  props: ['name', 'role'],
  template: `
    <div class="card">
      <h2>{{ name }}</h2>
      <p>{{ role }}</p>
    </div>
  `
})

app.mount('#app')
</script>
```

> 🔎 Les props rendent ton composant dynamique et réutilisable.

---

## 🔄 4. Remonter des infos vers le parent : les **events personnalisés**

Pour faire remonter une action du composant enfant vers le parent, on utilise `$emit()`.

### Exemple :

```html
<div id="app">
  <like-button @liked="count++"></like-button>
  <p>❤️ Likes : {{ count }}</p>
</div>

<script>
const app = Vue.createApp({
  data() {
    return { count: 0 }
  }
})

app.component('like-button', {
  template: `<button @click="$emit('liked')">J'aime 👍</button>`
})

app.mount('#app')
</script>
```

---

## 🧱 5. Structurer une mini app avec plusieurs composants

Imaginons une app de gestion de tâches :

- `App` (composant racine)
- `TaskList` (liste des tâches)
- `TaskItem` (chaque tâche)

```html
<div id="app">
  <task-list></task-list>
</div>

<script>
const app = Vue.createApp({})

app.component('task-item', {
  props: ['task'],
  template: `<li>{{ task }}</li>`
})

app.component('task-list', {
  data() {
    return {
      tasks: ['Apprendre Vue', 'Faire un café', 'Coder un projet']
    }
  },
  template: `
    <ul>
      <task-item v-for="(t, i) in tasks" :key="i" :task="t"></task-item>
    </ul>
  `
})

app.mount('#app')
</script>
```

---

## 🚀 Exercice pratique

🧩 **Exercice : Carte de profil dynamique**

Crée un composant `<user-card>` avec :  
- Une prop `name` et une prop `age`  
- Un bouton “+1 an” qui incrémente l’âge (en émettant un event)  
- Le composant parent qui écoute cet event et met à jour la donnée

💡 Astuce : tu auras besoin de `$emit()` et `v-on` (`@`)

---

## 🏁 À retenir

| Concept | Description |
|---------|-------------|
| Composant | Bloc réutilisable contenant son HTML, JS, CSS |
| Props | Permettent de passer des données du parent à l’enfant |
| Events (`$emit`) | Permettent de faire remonter des actions vers le parent |
| Structure modulaire | Facilite la maintenance et la clarté du code |

---

🎓 **Prochain cours :** Les transitions et animations avec Vue.js ✨

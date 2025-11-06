# 🧠 Cours 2 — Les directives et l’interactivité dans Vue.js

---

## 🎯 Objectifs du cours

À la fin de ce cours, tu sauras :

✅ Manipuler les **directives Vue.js** (`v-if`, `v-for`, `v-bind`, `v-on`, etc.)  
✅ Comprendre comment **lier dynamiquement les données** à ton interface  
✅ Gérer les **événements utilisateurs**  
✅ Créer un **mini projet interactif complet** : une liste de tâches

---

## 🧩 1. Qu’est-ce qu’une directive Vue.js ?

Les **directives** sont des **attributs spéciaux** dans le HTML, précédés du préfixe `v-`.  
Elles indiquent à Vue qu’il doit **réagir ou modifier le DOM** selon les données.

### 🔹 Exemple simple : `v-text` et `v-html`

```html
<div id="app">
  <p v-text="message"></p>
  <p v-html="htmlMessage"></p>
</div>

<script>
const app = Vue.createApp({
  data() {
    return {
      message: "Bonjour depuis Vue !",
      htmlMessage: "<b>Texte en gras</b>"
    };
  }
}).mount('#app');
</script>
```

---

## 🧩 2. Le data binding : `v-bind`

La directive `v-bind` relie une **propriété HTML** à une **valeur dynamique**.  
Elle peut être raccourcie avec le symbole `:`.

### 🔹 Exemple

```html
<div id="app">
  <img v-bind:src="imageUrl" alt="Image dynamique">
  <!-- raccourci -->
  <img :src="imageUrl" alt="Image dynamique">
</div>

<script>
const app = Vue.createApp({
  data() {
    return {
      imageUrl: "https://picsum.photos/200"
    };
  }
}).mount('#app');
</script>
```

---

## 🧩 3. Les conditions : `v-if`, `v-else-if`, `v-else`, `v-show`

Ces directives permettent d’**afficher ou non** un élément selon une condition.

### 🔹 Exemple

```html
<div id="app">
  <p v-if="isLoggedIn">Bienvenue, utilisateur !</p>
  <p v-else>Veuillez vous connecter.</p>

  <!-- v-show masque seulement via CSS (display:none) -->
  <p v-show="showInfo">Informations visibles sans supprimer le DOM</p>
</div>

<script>
const app = Vue.createApp({
  data() {
    return {
      isLoggedIn: false,
      showInfo: true
    };
  }
}).mount('#app');
</script>
```

> 💡 `v-if` **supprime l’élément du DOM**, tandis que `v-show` **le cache simplement**.

---

## 🧩 4. Les boucles : `v-for`

Permet de **répéter un élément HTML** pour chaque item d’un tableau ou d’un objet.

### 🔹 Exemple

```html
<div id="app">
  <ul>
    <li v-for="(fruit, index) in fruits" :key="index">
      {{ index + 1 }}. {{ fruit }}
    </li>
  </ul>
</div>

<script>
const app = Vue.createApp({
  data() {
    return {
      fruits: ["Pomme", "Banane", "Cerise"]
    };
  }
}).mount('#app');
</script>
```

---

## 🧩 5. Les événements : `v-on` (ou `@`)

Permet de **réagir à des actions utilisateur** (clic, saisie clavier, etc.).

### 🔹 Exemple

```html
<div id="app">
  <button v-on:click="increment">Cliquez-moi</button>
  <!-- raccourci -->
  <button @click="increment">+1</button>

  <p>Compteur : {{ count }}</p>
</div>

<script>
const app = Vue.createApp({
  data() {
    return {
      count: 0
    };
  },
  methods: {
    increment() {
      this.count++;
    }
  }
}).mount('#app');
</script>
```

---

## 🧩 6. Combiner les directives

On peut **combiner plusieurs directives** dans un même élément.

### 🔹 Exemple

```html
<div id="app">
  <ul>
    <li 
      v-for="(task, index) in tasks" 
      :key="index"
      v-show="!task.done"
      @click="markDone(index)"
    >
      {{ task.name }}
    </li>
  </ul>
</div>

<script>
const app = Vue.createApp({
  data() {
    return {
      tasks: [
        { name: "Faire les courses", done: false },
        { name: "Aller courir", done: false },
        { name: "Coder un projet Vue", done: false }
      ]
    };
  },
  methods: {
    markDone(index) {
      this.tasks[index].done = true;
    }
  }
}).mount('#app');
</script>
```

---

## 🧩 7. 🧪 Exercice pratique — Mini projet : "Liste de tâches"

### 🎯 Objectif

Créer une application où l’utilisateur peut :
- Ajouter une tâche
- Lister les tâches
- Marquer une tâche comme faite

### 🧱 Étapes

1. Crée un fichier `index.html`  
2. Copie la structure suivante :

```html
<div id="app">
  <h2>📝 Ma liste de tâches</h2>

  <input type="text" v-model="newTask" placeholder="Nouvelle tâche">
  <button @click="addTask">Ajouter</button>

  <ul>
    <li 
      v-for="(task, index) in tasks" 
      :key="index" 
      @click="toggleTask(index)"
      :class="{ done: task.done }"
    >
      {{ task.text }}
    </li>
  </ul>
</div>

<script src="https://unpkg.com/vue@3"></script>
<script>
const app = Vue.createApp({
  data() {
    return {
      newTask: '',
      tasks: []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, done: false });
        this.newTask = '';
      }
    },
    toggleTask(index) {
      this.tasks[index].done = !this.tasks[index].done;
    }
  }
}).mount('#app');
</script>

<style>
.done {
  text-decoration: line-through;
  color: gray;
}
</style>
```

### 🧠 À retenir

- `v-model` permet de **lier un champ input** à une variable (`newTask`)
- `v-for` affiche la liste des tâches
- `@click` réagit aux clics
- Les données se mettent à jour automatiquement sans toucher au DOM 🎉

---

## 🚀 Pour aller plus loin

- Essaie d’ajouter un bouton 🗑️ pour **supprimer une tâche**
- Garde les tâches dans le **localStorage** du navigateur
- Ajoute un **compteur** de tâches terminées

---

## 📚 Résumé

| Directive | Rôle | Raccourci |
|------------|------|------------|
| `v-bind` | Lie une donnée à un attribut HTML | `:` |
| `v-on` | Gère un événement | `@` |
| `v-if / v-else / v-show` | Affiche ou cache un élément | — |
| `v-for` | Répète un élément pour chaque item | — |
| `v-model` | Lie un champ de formulaire à une donnée | — |

---

> 🔥 Prochain cours : **Cours 3 — Les composants et la structure d’une application Vue.js**

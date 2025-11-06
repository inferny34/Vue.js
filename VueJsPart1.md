# 🧠 Cours 1 — Introduction à Vue.js + Premier projet interactif

---

## 🎯 Objectifs du cours
À la fin de ce cours, tu sauras :

✅ Ce qu’est Vue.js et pourquoi on l’utilise  
✅ Comment l’intégrer dans une page HTML  
✅ Comment relier les données à ton HTML (data binding)  
✅ Comment réagir à des actions utilisateur (events)  
✅ Créer ta **première mini app Vue interactive**

---

## 🧩 1. Qu’est-ce que Vue.js ?

**Vue.js** est un framework JavaScript pour construire des **interfaces dynamiques**.  
Il te permet de relier ton HTML au JavaScript facilement, sans avoir à manipuler le DOM manuellement (comme avec jQuery).

> 🔍 En clair : tu dis à Vue ce que tu veux afficher, il s’occupe du “comment”.

### 🟩 Exemple comparatif

**Sans Vue :**
```js
document.getElementById("message").textContent = "Bonjour";
```

**Avec Vue :**
```html
<p>{{ message }}</p>
```
```js
data() {
  return { message: "Bonjour" }
}
```

🧠 C’est **réactif** : si la variable `message` change, le texte se met à jour automatiquement !

---

## ⚙️ 2. Installation rapide

Tu n’as rien besoin d’installer pour commencer.

Crée un dossier `vue-intro`, puis un fichier `index.html` à l’intérieur :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Première app Vue</title>
</head>
<body>
  <div id="app">
    <h1>{{ message }}</h1>
    <button @click="changerMessage">Changer le message</button>
  </div>

  <!-- Import de Vue depuis un CDN -->
  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

  <script>
    // On crée une application Vue
    const app = Vue.createApp({
      // Données de l’application
      data() {
        return {
          message: "Bonjour depuis Vue.js 😄"
        }
      },
      // Méthodes (fonctions disponibles dans le HTML)
      methods: {
        changerMessage() {
          this.message = "Le message a changé 🎉"
        }
      }
    })

    // On "monte" l'app sur le <div id="app">
    app.mount("#app")
  </script>
</body>
</html>
```

---

## 🔍 3. Décortiquons le code

| Élément | Rôle |
|----------|------|
| `<div id="app">` | Conteneur de ton application Vue |
| `{{ message }}` | Interpolation : affiche la variable `message` |
| `@click="changerMessage"` | Événement Vue : appelle la méthode `changerMessage()` |
| `Vue.createApp({ ... })` | Crée une instance d’application Vue |
| `app.mount("#app")` | Connecte Vue à ton HTML |

---

## 💬 4. Les “must-know” du langage Vue

### ✅ Interpolation (afficher une donnée)
```html
<p>{{ username }}</p>
```

### ✅ Liaison d’attribut (`v-bind`)
```html
<img v-bind:src="photo">
<!-- ou raccourci -->
<img :src="photo">
```

### ✅ Gestion d’événements (`@click`)
```html
<button @click="saluer">Dire bonjour</button>
```

### ✅ Données réactives
```js
data() {
  return { compteur: 0 }
}
```
```html
<p>{{ compteur }}</p>
<button @click="compteur++">+1</button>
```

---

## 🧠 5. Exercice pratique : compteur réactif

Ajoute ce code complet dans ton `index.html` (remplace le précédent) :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Compteur Vue.js</title>
  <style>
    body { font-family: sans-serif; text-align: center; margin-top: 50px; }
    button { padding: 10px 20px; margin: 5px; font-size: 18px; }
  </style>
</head>
<body>
  <div id="app">
    <h1>🧮 Compteur Vue.js</h1>
    <h2>{{ compteur }}</h2>
    <button @click="incrementer">+1</button>
    <button @click="decrementer">-1</button>
    <button @click="reset">Reset</button>
  </div>

  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
  <script>
    const app = Vue.createApp({
      data() {
        return {
          compteur: 0
        }
      },
      methods: {
        incrementer() {
          this.compteur++
        },
        decrementer() {
          this.compteur--
        },
        reset() {
          this.compteur = 0
        }
      }
    })
    app.mount("#app")
  </script>
</body>
</html>
```

✅ Ouvre le fichier dans ton navigateur  
➡️ Clique sur les boutons  
➡️ Observe comment les données se mettent à jour automatiquement.

---

## 🔧 6. Challenge supplémentaire (facultatif)

Améliore le compteur :
- Ajoute un champ `<input v-model="pas">` pour changer la valeur d’incrémentation.  
- Multiplie le compteur par 2 avec un bouton “x2”.

👉 Exemple d’idée :
```html
<input v-model.number="pas" type="number" min="1">
<button @click="incrementer">+{{ pas }}</button>
```

---

## 🧭 7. Ce que tu as appris

| Concept | Description |
|----------|--------------|
| **Instance Vue** | L’objet qui contrôle une partie de ta page |
| **`data()`** | Contient les variables de ton application |
| **`methods`** | Contient les fonctions appelées depuis le HTML |
| **Interpolation** | `{{ variable }}` affiche la valeur d’une variable |
| **Directives Vue** | `v-bind`, `v-model`, `v-for`, `v-if`, `@click`, etc. |

---

## 🚀 8. À suivre — Cours 2 : Conditions, boucles et formulaires

Dans le prochain cours, nous verrons :

- Créer une **liste de tâches complète**
- Découvrir `v-if`, `v-for` et `v-model`
- Supprimer / ajouter dynamiquement des éléments
- Gérer la réactivité avancée avec les événements

---

🧩 **Auteur :** _Cours interactif créé par inferny34_  
📘 **Projet :** Formation Vue.js — Niveau Débutant → Avancé  
🕹️ **Mini-projet du cours :** Compteur réactif  
📅 **Version :** 1.0

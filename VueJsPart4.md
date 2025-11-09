# 🧠 Cours 4 — Les transitions et animations avec Vue.js ✨

---

## 🎯 Objectifs du cours

À la fin de ce cours, tu sauras :

✅ Utiliser la balise `<transition>` de Vue.js  
✅ Ajouter des animations CSS à l’apparition / disparition d’éléments  
✅ Créer des transitions dynamiques contrôlées par le JavaScript  
✅ Enchaîner plusieurs effets et gérer les états d’animation

---

## 🧩 1. Comprendre les transitions Vue.js

Vue.js rend les transitions **très simples** grâce à la balise `<transition>`.  
Elle s’applique quand un élément **entre ou sort du DOM** (par exemple avec `v-if`, `v-show`, etc.).

### Exemple basique

```html
<div id="app">
  <button @click="visible = !visible">Afficher / Cacher</button>
  <transition name="fade">
    <p v-if="visible">Coucou 👋</p>
  </transition>
</div>

<script>
const app = Vue.createApp({
  data() {
    return { visible: true }
  }
}).mount("#app")
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
```

💡 Ici :
- `.fade-enter-active` et `.fade-leave-active` définissent la **durée / style global** de la transition.  
- `.fade-enter-from` et `.fade-leave-to` indiquent **l’état de départ et de sortie**.

---

## 🎬 2. Les classes utilisées par Vue.js

Quand un élément apparaît ou disparaît, Vue applique automatiquement ces classes :

| Phase | Classe appliquée |
|-------|------------------|
| Entrée (début) | `.v-enter-from` |
| Entrée (active) | `.v-enter-active` |
| Entrée (fin) | `.v-enter-to` |
| Sortie (début) | `.v-leave-from` |
| Sortie (active) | `.v-leave-active` |
| Sortie (fin) | `.v-leave-to` |

> Si tu donnes un nom à ta transition (`<transition name="fade">`), Vue remplacera `v-` par `fade-`.

---

## 🌀 3. Personnaliser les transitions avec JavaScript

Tu peux aussi contrôler les transitions **avec du code JS**, par exemple pour lancer une animation après un certain délai :

```html
<transition
  @before-enter="beforeEnter"
  @enter="enter"
  @leave="leave">
  <p v-if="visible">Salut 😎</p>
</transition>

<script>
const app = Vue.createApp({
  data() {
    return { visible: true }
  },
  methods: {
    beforeEnter(el) {
      el.style.opacity = 0
    },
    enter(el, done) {
      setTimeout(() => {
        el.style.transition = "opacity 1s"
        el.style.opacity = 1
        done()
      }, 200)
    },
    leave(el, done) {
      el.style.transition = "opacity 0.5s"
      el.style.opacity = 0
      setTimeout(done, 500)
    }
  }
}).mount("#app")
</script>
```

---

## 🧱 4. Gérer plusieurs éléments avec `<transition-group>`

Si tu veux animer une **liste d’éléments** (ex: une todo list), utilise `<transition-group>`.

```html
<div id="app">
  <button @click="addItem">Ajouter</button>
  <transition-group name="list" tag="ul">
    <li v-for="(item, i) in items" :key="item">{{ item }}</li>
  </transition-group>
</div>

<script>
const app = Vue.createApp({
  data() {
    return { items: [1, 2, 3] }
  },
  methods: {
    addItem() {
      this.items.push(this.items.length + 1)
    }
  }
}).mount("#app")
</script>

<style>
.list-enter-active, .list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from, .list-leave-to {
  opacity: 0;
  transform: translateY(20px);
}
</style>
```

🪄 Les éléments apparaissent / disparaissent avec une **translation fluide et un fondu**.

---

## 🧠 En résumé

- `<transition>` : pour un seul élément.  
- `<transition-group>` : pour des listes.  
- Utilise les classes `.v-enter-*` et `.v-leave-*` ou les hooks JS (`@enter`, `@leave`…).  
- Combine les effets CSS et JS pour des transitions dynamiques et fluides.

---

💪 **Exercice pratique** :
Crée une petite carte d’information qui apparaît en fondu et s’agrandit légèrement quand on clique sur un bouton.

🎯 Bonus : ajoute un effet inverse quand elle disparaît !

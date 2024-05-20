<script setup>

const props = defineProps({
  troupe: { //Nom de la propriété
    type: Object, //Type de la propriété
    required: true //Propriété obligatoire
  },
  or: {
    type: Number,
    required: true
  }
})

const emit = defineEmits(["former"]);

const formerTroupe = (troupe) => {
  emit("former", troupe);
};

</script>

<template>
  <article>
    <header :style="'background: linear-gradient(60deg,#3B3B3B 0%,' + troupe.couleur + ' 100%);'">
      <img :src="troupe.image"
           :alt="troupe.nom">
    </header>
    <div class="level" :style="'color: ' + troupe.couleur + ';'">
      Niveau {{troupe.niveau}}
    </div>
    <h2 class="name">{{ troupe.nom }}</h2>
    <button
        :style="'background-color: ' + troupe.couleur + ';'"
        @click="formerTroupe(troupe)"
        :disabled="or < troupe.cout"
    >
        Former
        <img src="/public/img/piece-or.png" alt="Former">
    </button>
    <router-link to="/troupe-fiche">
      <button>Consulter les détails</button>
    </router-link>
    <p class="description">{{troupe.description }}</p>
    <footer>
      <div class="training"
           :style="'background-color: ' + troupe.couleur + ';'">
        <div>{{troupe.formation}}<sup>sec</sup></div>
        <div>Formation</div>
      </div>
      <div class="speed"
           :style="'background-color: ' + troupe.couleur + ';'">
        <div>{{troupe.vitesse}}</div>
        <div>Vitesse</div>
      </div>
      <div class="cost"
           :style="'background-color: ' + troupe.couleur + ';'">
        <div>{{troupe.cout}}</div>
        <div>Coût</div>
      </div>
    </footer>
  </article>
</template>

<style scoped>

</style>
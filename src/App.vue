<script setup>
// Cheat Sheet: https://steve-fallet.notion.site/Vue-3-script-setup-Cheat-Sheet-b12192ceae244ecda65f771579ca02bc
import {onMounted, ref} from 'vue'
import PageTopBarre from "@/components/PageTopBarre.vue";
import PageHeader from "@/components/PageHeader.vue";
import PageFooter from "@/components/PageFooter.vue";

// Tableau des troupes
const troupes = ref([])

//Déclaration de variables
let totalOr = ref(100000);

// Quand le composant est monté, on va chercher les données
onMounted(() => {
  fetch('https://cocapi.divtec.me/troupes') //Appel à l'API
      .then((reponseAPI) => reponseAPI.json())  //Récupération des données au format .json et transformation en objet JavaScript
      .then((donneesFormatJS) => { //Récupération des données au format JavaScript
        troupes.value = donneesFormatJS //Stockagge dans la variable troupes
      })
})
</script>

<template>
<PageTopBarre :or="totalOr"/>
  <header>
    <PageHeader/>
  </header>
  <main>
    <ul class="cartes">
      <li v-for="troupe in troupes" :key="troupe">
        <article>
          <header :style="'background: linear-gradient(60deg,#3B3B3B 0%, ' + troupe.couleur + ' 100%);'">
            <img :src="troupe.image"
                 :alt="troupe.nom">
          </header>
          <div class="level" :style="'color: ' + troupe.couleur + ';'">
            Niveau {{troupe.niveau}}
          </div>
          <h2 class="name">{{ troupe.nom }}</h2>
          <button :style="'background-color: ' + troupe.couleur + ';'"> Former
            <img src="/img/piece-or.png" alt="Former"></button>
          <p class="description">
            {{troupe.description}}</p>
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
      </li>
    </ul>
  </main>
  <footer>
    <PageFooter/>
  </footer>
</template>

<style scoped lang="sass">

</style>
<script setup>
// Cheat Sheet: https://steve-fallet.notion.site/Vue-3-script-setup-Cheat-Sheet-b12192ceae244ecda65f771579ca02bc
import {onMounted, ref} from 'vue'
import PageTopBarre from "@/components/PageTopBarre.vue";
import PageHeader from "@/components/PageHeader.vue";
import PageFooter from "@/components/PageFooter.vue";
import TroupeCarte from "@/components/TroupeCarte.vue";

// Tableau des troupes
const troupes = ref([])

//Déclaration de variables
let totalOr = ref(100000);

let troupesFormees = ref(0);

// Quand le composant est monté, on va chercher les données
onMounted(() => {
  fetch('https://cocapi.divtec.me/troupes') //Appel à l'API
      .then((reponseAPI) => reponseAPI.json())  //Récupération des données au format .json et transformation en objet JavaScript
      .then((donneesFormatJS) => { //Récupération des données au format JavaScript
        troupes.value = donneesFormatJS //Stockagge dans la variable troupes
      })
})

/*Méthodes */
/* Méthodes */
function formerTroupe(troupe) {
  if (totalOr.value < troupe.cout) {
    alert("Vous n'avez pas assez d'or mon seigneur !")
    return
  }
  totalOr.value -= troupe.cout
  //troupesFormees.value.push(troupe)
  troupesFormees.value ++;
}

</script>

<template>
  <router-view/>
<PageTopBarre :or="totalOr" :troupe-formees="troupesFormees"/>
    <PageHeader/>
  <main>
    <ul class="cartes">
      <li v-for="troupe in troupes" :key="troupe">
        <TroupeCarte
            :troupe="troupe"
            :or="totalOr"
            @former="formerTroupe"
        />
      </li>
    </ul>
  </main>
    <PageFooter/>
</template>

<style scoped lang="sass">

</style>
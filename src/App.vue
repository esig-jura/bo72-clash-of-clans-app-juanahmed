<script setup>
// Cheat Sheet: https://steve-fallet.notion.site/Vue-3-script-setup-Cheat-Sheet-b12192ceae244ecda65f771579ca02bc
//import {ref} from 'vue'
import {onMounted, ref} from 'vue'
import PageTopBarre from "@/components/PageTopBarre.vue";
import PageHeader from "@/components/PageHeader.vue";
import PageFooter from "@/components/PageFooter.vue";
import TroupeCarte from "@/components/TroupeCarte.vue";

// Tableau des troupes
const troupes = ref([]);

//Pièces d'or
let totalOr = ref(20000);

let nbTroupesFormees = ref(0);

// Quand le composant est monté, on va chercher les données
onMounted(() => {
  fetch('https://cocapi.divtec.me/troupes') //Appel à l'API
      .then((reponseAPI) => reponseAPI.json())  //Récupération des données au format .json et transformation en objet JavaScript
      .then((donneesFormatJS) => { //Récupération des données au format JavaScript
        troupes.value = donneesFormatJS //Stockagge dans la variable troupes
      })
})

/* Méthodes */
function formerTroupe(troupe) {
  if (totalOr.value < troupe.cout) {
    alert("Vous n'avez pas assez d'or mon seigneur !")
    return
  }
  totalOr.value -= troupe.cout
  nbTroupesFormees.value += 1;
}

</script>

<template>
  <router-view/>
  <page-top-barre :or="totalOr" :troupeFormees="nbTroupesFormees"/>
    <page-header/>
  <main>
    <ul class="cartes">
      <li v-for="troupe in troupes">
        <troupe-carte
            :or="totalOr"
            :troupe="troupe"
            @former="formerTroupe"
        />
      </li>
    </ul>
  </main>
<page-footer/>
</template>
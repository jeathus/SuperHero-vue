<script setup>
import axios from "axios";
import { computed, onMounted, ref } from "vue";

// Déclarations des variables réactives
const superheros = ref([]);
const afficherPouvoirs = ref(false);
const filteredSuperheros = ref(""); // Variable de filtrage

// Chargement des données depuis l'API au montage du composant
onMounted(() => {
  axios
    .get(
      "https://cdn.jsdelivr.net/gh/rtomczak/superhero-api@0.3.0/api/all.json"
    )
    .then((response) => {
      superheros.value = response.data; // Récupération des superhéros
    })
    .catch((error) => {
      console.log(error); // Gestion d'erreur en cas de problème avec l'API
    });
});

// Filtrage des superhéros selon la requête de recherche
const filteredData = computed(() => {
  if (!filteredSuperheros.value) return superheros.value;
  return superheros.value.filter((item) =>
    item.name.toLowerCase().startsWith(filteredSuperheros.value.toLowerCase())
  );
});
</script>

<template>
  <div id="app">
    <Navbar />
    <router-view />

    <!-- Titre de la page -->
    <h2 class="my-4 text-center">Liste des superhéros</h2>

    <!-- Checkbox pour afficher ou non les pouvoirs -->
    <div class="my-4 text-center">
      <input
        type="checkbox"
        v-model="afficherPouvoirs"
        id="afficherPouvoirs"
        class="form-check-input"
      />
      <label class="form-check-label text-primary" for="afficherPouvoirs"
        >Afficher les pouvoirs</label
      >
    </div>

    <!-- Champ de recherche -->
    <input
      type="search"
      class="form-control me-2"
      v-model="filteredSuperheros"
      placeholder="Rechercher un Super Héro"
    />

    <!-- Bouton de réinitialisation de la recherche -->
    <div v-if="filteredSuperheros">
      <button class="btn btn-primary my-2" v-on:click="filteredSuperheros = ''">
        Réinitialiser
      </button>
    </div>

    <!-- Liste filtrée des superhéros -->
    <ul class="list-group">
      <li
        v-for="item in filteredData"
        :key="item.id"
        class="list-group-item list-group-item-action d-flex justify-content-between align-items-center w-100"
      >
        <img
          :src="item.images.sm"
          alt="superheroImage"
          class="me-3 rounded-circle"
        />
        <h5 class="mb-0">{{ item.name }}</h5>
        <small>{{ item.id }}</small>

        <!-- Affichage conditionnel des pouvoirs -->
        <div v-if="afficherPouvoirs">
          <p>
            Intelligence : {{ item.powerstats.intelligence }}<br />
            Force : {{ item.powerstats.strength }}<br />
            Vitesse : {{ item.powerstats.speed }}<br />
            Durabilité : {{ item.powerstats.durability }}<br />
            Puissance : {{ item.powerstats.power }}<br />
            Combat : {{ item.powerstats.combat }}
          </p>
        </div>
      </li>
    </ul>
  </div>
</template>

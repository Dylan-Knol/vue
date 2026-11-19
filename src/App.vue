<script setup>
import { ref } from 'vue'

// Hier worden de variabelen aangemaakt die de taken opslaan.
const taken = ref([]);
const nieuwetaak = ref("");
// Deze functie voegt een nieuwe taak toe aan de lijst.
const addTask = () => {
  // Controleert of het invoerveld niet leeg is.
  if (nieuwetaak.value.trim() !== "") {
    taken.value.push(nieuwetaak.value);
    nieuwetaak.value = "";
  }
};
// Deze functie verwijdert een taak uit de lijst.
const taakVerwijderen = (index) => {
  taken.value.splice(index, 1);
};
</script>
<template>
  <!-- Dit is de achtergrond en de hoofdcontainer van de pagina. -->
  <div class="fixed inset-0 w-screen h-screen overflow-auto bg-slate-100">
    <div class="w-full min-h-full bg-white p-12">
      <!-- Titel en korte uitleg van de takenlijst. -->
      <h1 class="text-4xl font-bold text-slate-800 mb-2">
        Mijn takenlijst
      </h1>
      <p class="text-slate-500 mb-8 text-lg">
        Houd je taken overzichtelijk op één plek.
      </p>
      <!-- Hier kan de gebruiker een nieuwe taak invullen en toevoegen. -->
      <div class="flex gap-3 mb-8 w-full">
        <input
          v-model="nieuwetaak"
          @keyup.enter="addTask"
          placeholder="Voeg een nieuwe taak toe..."
          class="flex-1 min-w-0 bg-white text-slate-900 placeholder:text-slate-500 border border-slate-300 rounded-lg px-5 py-4 text-lg outline-none focus:ring-2 focus:ring-blue-500"
        />
        <button
          @click="addTask"
          class="bg-blue-600 hover:bg-blue-700 text-white font-semibold px-8 rounded-lg transition text-lg"
        >
          + Toevoegen
        </button>
      </div>
      <!-- Hier wordt het aantal toegevoegde taken weergegeven. -->
      <h2 class="text-xl font-semibold text-slate-700 mb-4">
        Mijn taken ({{ taken.length }})
      </h2>
      <!-- v-for zorgt ervoor dat alle taken automatisch worden weergegeven. -->
      <ul class="space-y-3 w-full">
        <li
          v-for="(taak, index) in taken"
          :key="index"
          class="flex items-center justify-between bg-slate-50 border border-slate-200 rounded-lg p-5"
        >
          <span class="text-slate-700 text-lg">
            {{ taak }}
          </span>
          <!-- Met deze knop kan een taak weer verwijderd worden. -->
          <button
            @click="taakVerwijderen(index)"
            class="text-red-500 hover:text-red-700 font-medium transition"
   >
            Verwijderen
          </button>
        </li>
      </ul>
      <!-- Deze tekst verschijnt alleen wanneer er nog geen taken zijn. -->
      <p v-if="taken.length === 0" class="text-center text-slate-400 py-8">
        Je hebt nog geen taken toegevoegd.
      </p>
    </div>
  </div>
</template>
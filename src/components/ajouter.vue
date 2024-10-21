<template>
  <label for="">Entrez le nom de la tâche: </label>
  <input type="text" name="nomTache" id="" v-model="nomTache" />
  <br /><br />
  <label for="">Entrez l'état de la tâche (true or false): </label>
  <input type="text" v-model="etat" />
  <br /><br />
  <button @click="Ajouter">Ajouter</button>
  <br /><br />
  <RouterLink :to="{ name: 'Accueil' }"> Retour à l'accueil</RouterLink>
</template>
<script setup>
import { ref, defineEmits, computed, watch } from "vue";
import json from "@/assets/todolist.json";

let data = ref(json);
const nomTache = ref();
const etat = ref();

let nomTacheCalcule = computed(() => nomTache.value);
let etatCalcule = computed(() => etat.value);
let id = ref(data.value.length + 1);

watch(id, (newValue, oldValue) => {
  console.log("new id valeur : " + newValue);
  console.log("old id value : " + oldValue);

  id.value++;
  console.log("id value after incrementation : " + id.value);
});

function Ajouter() {
  let obj = {
    id: id.value++,
    task: nomTacheCalcule,
    completed: etatCalcule,
  };
  data.value.push(obj);
  console.log(id.value);
}
</script>

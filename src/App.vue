<script setup>
import {computed, ref} from "vue";

const newImageUrl = ref("");
const images = ref(["https://images.radio-canada.ca/q_auto,w_1250/v1/ici-info/16x9/rick-astley-videoclip-never-gonna-give-you-up.png"]);

const isButtonDisabled = computed(() => !newImageUrl.value.trim() || !(newImageUrl.value.startsWith("http://") || newImageUrl.value.startsWith("https://")));
//startwith est une méthode JS comme trim (note à moi même approfondir les méthodes JS)
const totalImages = computed(() => images.value.length);

function addImage() {
  if (newImageUrl.value.trim()) {
    images.value.push(newImageUrl.value);
    newImageUrl.value = "";
  }
}

</script>

<template>
  <div class="container">
    <h1>Galerie d'Images</h1>
    <div class="containerInput">
      <input
          type="text"
          class="inputUrl"
          v-model="newImageUrl"
          placeholder="Entrez l'URL d'une nouvelle image">
      <button @click="addImage" class="boutonAjouter" :disabled="isButtonDisabled">Ajouter un lien d'image</button>
    </div>
  </div>

  <div class="stats">
    Nombre total d'images : {{ totalImages }}
  </div>

  <div class="container gallery">

    <!--- Galerie d'image avec un bouton supprimer pour chaque image-->
    <div>
      <div v-for="(image, index) in images" :key="index" class="image-container">
        <img :src="image" alt="image" class="imageTaille"/>
        <button class="boutonSupprimer" @click="images.splice(index, 1)">Supprimer l'image</button>
      </div>
      <h1 v-if="totalImages === 0">Aucune image d'ajoutée !!!</h1>
    </div>
  </div>
</template>

<style scoped>

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}
.container h1{
  color:white;
}
.image-container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}
.gallery {
  display: flex;
  flex-direction: column;
}

.stats {
  display: flex;
  font-size: 1.5em;
  justify-content: center;
  align-items: center;
  margin-top: 30px;
  color: white;
}

.imageTaille {
  width: 300px;
  height: 300px;
  border-radius: 30%;
}
.boutonSupprimer {
  background-color: red;
  color: white;
  border: none;
  padding: 10px 20px;
  margin-top: 10px;
  border-radius: 10px;
}
.boutonAjouter{
  background-color: green;
  color: white;
  padding: 10px 20px;
  margin-top: 10px;
  border-radius: 10px;
}
.inputUrl{
  padding: 10px 20px;
  border-radius: 10px;
}
.containerInput{
  display: flex;
  flex-direction: column;
}
</style>

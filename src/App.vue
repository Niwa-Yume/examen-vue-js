<script setup>
import {computed, ref} from "vue";

const newImageUrl = ref("");
const images = ref(["https://images.radio-canada.ca/q_auto,w_1250/v1/ici-info/16x9/rick-astley-videoclip-never-gonna-give-you-up.png"]);
const isButtonDisabled = computed(() => !newImageUrl.value.trim());


function addImage() {
  if (newImageUrl.value.trim()) {
    images.value.push(newImageUrl.value);
    newImageUrl.value = "";
  }
}

</script>

<template>
  <div class="container gallery">
    <h1>Galerie d'Images</h1>

    <!--- Galerie d'image avec un bouton supprimer pour chaque image-->
    <div>
      <div v-for="(image, index) in images" :key="index" class="image-container">
        <img :src="image" alt="image" class="imageTaille"/>
        <button class="boutonSupprimer" @click="images.splice(index, 1)">Supprimer</button>
      </div>
    </div>
  </div>


  <div class="container">
    <input
        type="text"
        v-model="newImageUrl"
        placeholder="Entrez l'URL d'une image"
        @keyup.enter="addImage"
    >
    <button @click="addImage" :disabled="isButtonDisabled">Ajouter</button>
  </div>

  <div class="stats">
    Nombre total d'images : {{ images.length }}
  </div>

  <div class="gallery">

  </div>
</template>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
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
  justify-content: center;
}

.stats {
  font-size: 1.5em;
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
  cursor: pointer;
  border-radius: 10px;
}
</style>

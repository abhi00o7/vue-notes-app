<script setup>
import { ref } from "vue";

const showModal = ref(false);
const textAreaInput = ref("");
const notes = ref([]);
const errorMessage = ref("");
/**
 *
 * @param {array of objects} notes
 */

const randomLightColor = () =>
  `hsl(${Math.floor(Math.random() * 361)}, 100%, 75%)`;

const randomNumber = (min, max) =>
  Math.floor(Math.random() * (max - min + 1) + min);

const closeModal = () => {
  textAreaInput.value = ``;
  errorMessage.value = ``;
  showModal.value = false;
};
const addNote = () => {
  if (!textAreaInput.value)
    return (errorMessage.value = `Note can not be less than 1 characters.`);

  notes.value.push({
    id: randomNumber(10000, 99999),
    text: textAreaInput.value,
    color: randomLightColor(),
    date: new Date().toLocaleString(),
  });

  textAreaInput.value = errorMessage.value = ``;
  showModal.value = false;
};
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea
          v-model.trim="textAreaInput"
          name="note"
          id="note"
          cols="30"
          rows="10"
        ></textarea>
        <p v-if="errorMessage" class="errorField">
          {{ errorMessage }}
        </p>
        <button @click="addNote" @keyup.ctrl.enter="addNote">Add Note</button>
        <button class="close" @click="closeModal">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div
          v-for="note in notes"
          :key="note.id"
          class="card"
          :style="`background-color:${note.color}`"
        >
          <p class="main-text">
            {{ note.text }}
          </p>
          <p class="date">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.container {
  max-width: 1080px;
  padding: 10px;
  margin: 0 auto;
}
h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}
.card {
  width: 225px;
  height: 225px;
  background-color: rgb(161, 255, 230);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}
.main-text {
  line-height: 1.25;
  font-size: 17.5px;
  font-weight: bold;
}
.date {
  font-size: 12.5px;
  margin-top: auto;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  padding-bottom: 0;
}
header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  border-radius: 1080px;
  color: white;
  font-size: 20px;
}
.cards-container {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  padding-left: 20px;
}
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  transform: translate(-50%, -50%);
  top: 50%;
  left: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}
main {
  height: 100vh;
  width: 100vw;
}
.modal {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
}
.modal p {
  margin-left: auto;
  font-size: 20px;
  z-index: 100000;
  cursor: pointer;
}
textarea {
  width: 100%;
  height: 200px;
  padding: 5px;
  font-size: 20px;
}
.modal .close {
  background-color: #f00;
  margin-top: 7px;
}
.modal .errorField {
  color: #f00;
}
</style>

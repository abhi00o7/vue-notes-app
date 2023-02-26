<script setup>
import { ref } from "vue";

const showModal = ref(false);
const textAreaInput = ref("");
const notes = ref([]);

/**
 *
 * @param {array of objects} notes
 */

const randomLightColor = () =>
  `hsl(${Math.floor(Math.random() * 361)}, 50%, 75%)`;

const randomNumber = (min, max) =>
  Math.floor(Math.random() * (max - min + 1) + min);

const addNote = () => {
  const note = {
    id: randomNumber(10000, 99999),
    text: textAreaInput.value,
    color: randomLightColor(),
    date: new Date().toLocaleString(),
  };
  console.log({ note });
  console.log({ notes });
  notes.value.push(note);
  console.log({ notes });
  textAreaInput.value = ``;
  showModal.value = false;
};
</script>
<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea
          v-model="textAreaInput"
          name="note"
          id="note"
          cols="30"
          rows="10"
        ></textarea>
        <button @click="addNote" @keyup.ctrl.enter="addNote">Add Note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        {{ notes }}
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div class="card">
          <p class="main-text">
            Lorem ipsum dolor sit, amet consectetur adipisicing elit. Impedit
            molestias amet id unde esse! Ut.
          </p>
          <p class="date"></p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
* {
  outline: 1px solid limegreen;
}
.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}
h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}
.card {
  outline: 1px solid red;
  width: 225px;
  height: 225px;
  background-color: rgb(161, 78, 230);
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
  border-radius: 1000px;
  color: white;
  font-size: 20px;
}
.cards-container {
  display: flex;
  flex-wrap: wrap;
  padding: 10px;
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
</style>

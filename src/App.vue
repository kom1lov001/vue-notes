<script setup>
import { ref } from "vue";

let showModal = ref(false);
let areatexts = ref("");
let noteCase = ref([]);

function randomHsl() {
  return "hsla(" + Math.random() * 360 + ", 100%, 50%, 1)";
}
const newAddNote = () => {
  noteCase.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: areatexts.value,
    date: new Date(),
    backgroundColor: randomHsl(),
  });
  showModal.value = false;
  areatexts.value = "";
};
// onMounted(() => {
// console.log(newAddNote);
// }),
</script>

<template>
  <div>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea
          class="textare"
          name="note"
          id="note"
          cols="30"
          rows="10"
          v-model="areatexts"
        ></textarea>
        <button @click="newAddNote">Add Notes</button>
        <button class="close" @click="showModal = !showModal">Close</button>
      </div>
    </div>

    <div class="container">
      <h1 class="notes">Notes</h1>
      <button class="addbutton" @click="showModal = !showModal">+</button>
    </div>
    <div class="card-container">
      <!-- {{ noteCase }} -->
      <div class="card">
        <div
          class="cardin"
          v-for="item of noteCase"
          :style="{ backgroundColor: item.backgroundColor }"
        >
          <p class="main-text">{{ item.text }}</p>
          <p class="date">{{ item.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.notes {
  color: white;
  opacity: 0.8;
}
.addbutton {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  outline: none;
  border: none;
  align-items: center;
  font-size: large;
  color: grey;
}
.container {
  display: flex;
  align-items: center;
  justify-content: space-around;
  min-width: 100%;
  background: gray;
  padding: 15px;
}
.card-container {
  max-width: 70%;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  height: 100%;
}
.cardin {
  position: relative;
  width: 225px;
  height: 225px;
  background: gray;
  padding: 10px;
  border-radius: 30px;
  display: flex;
  flex-flow: column;
}
.card {
  display: flex;
  flex-flow: wrap row;
  padding: 15px;
  gap: 10px;
}
.main-text {
  font-size: 16px;
  color: aliceblue;
}
.date {
  position: absolute;
  bottom: 5px;
  color: aliceblue;
}
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal {
  width: 750px;
  padding: 30px;
  background: white;
  border-radius: 10px;
  position: relative;
  display: flex;
  flex-direction: column;
  /* height: 400px; */
}
.modal button {
  padding: 10px 20px;
  position: relative;
  margin-top: 10px;
  width: 100%;
  border: none;
  border-radius: 10px;
  background: blueviolet;
  color: white;
}
.modal .close {
  background: red;
}
.textare {
  position: relative;
  /* outline: none; */
}
/* #app {
  & p {
    color: brown;
  }
  & defed {
    background: red;
  }
} */
</style>

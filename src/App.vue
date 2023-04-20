<template>
  <main>
    <div class="overlay" v-if="showModal">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errorMessage">{{errorMessage}}</p>
        <button @click="addNewNote">Add Note</button>
        <button class="close"  @click="showModal = false, newNote = ''">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
    </div>
    <div class="cards-container">
      <div class="card" v-for="note in notes" :key='note.id' :style="{backgroundColor: note.backgroundColor}">
        <p class="main-text">{{note.text}}</p>
        <p class="date">{{note.date}}</p>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";

const notes = ref([])

const showModal = ref(false)
const newNote = ref('')
const errorMessage = ref('')

function randomHsl() {
    return 'hsla(' + (Math.random() * 360) + ', 100%, 50%, 1)';
}

const addNewNote = () => {
  if (newNote.value.length < 10) {
  return errorMessage.value = 'Notes need to be 10 characters or more'
  } else {  
    notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date().toLocaleDateString("en-US"),
    backgroundColor: randomHsl()
    })
    errorMessage.value = ''
  }
 
  newNote.value = ''
  showModal.value = false
}

</script>

<style scoped>
  .container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto
  }

  h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }

  .card {
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
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
    width: 1000px;
    display: flex;
    margin: auto;
    padding-left: 20px;
    flex-wrap: wrap;
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
    color: red;
    z-index: 100000;
    cursor: pointer;
  }

  textarea {
    width: 100%;
    height: 200px;
    padding: 5px;
    font-size: 20px;
  }
</style>
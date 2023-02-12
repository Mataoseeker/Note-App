<script setup>
import { ref } from 'vue'
const showModal = ref(false)
const newNote = ref("")
const errorMessage = ref("")
const notes = ref([])

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  
}

const addNote = () => {
  if(newNote.value.length < 10){
    return errorMessage.value = "Note needs to be 10 characters or more"
  }
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor()
  })
 showModal.value = false;
  newNote.value = "";
  errorMessage.value = "";
}
</script>


<template>
  <main>
 <div v-if="showModal" class="overlay">
<div class="modal">
  <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
  <p v-if="errorMessage">{{ errorMessage }}</p>
  <button @click="addNote">Add note</button>
  <button  class="close" @click="showModal = false">Close</button>
</div>
</div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      
      <div class="cards-container">
        <div v-for="note in notes" 
        :key="note.id"
        class="card"
        :style="{backgroundColor: note.backgroundColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US")}}</p>
        </div>    
      </div>
    </div>
  </main>
</template>

<style scoped>
main{
  background-color: rgba(0,0,0,0.77);
}
main{
  height: 100vh;
  width: 100vw;
}
.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;       
}
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
 
}
h1{
  font-size: 55px;
  font-weight: bold;
  margin-bottom: 25px;
  color: white;
}
header button{
  font-size: 20px;
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  color: white;
  background-color: rgb(21,20,20);
  cursor: pointer;
  border-radius: 100%;
}
.cards-container{
  display: flex;
  flex-wrap: wrap;
}

.card{
  width: 225px;
  height: 225px;
  background-color: rgb(237,182,44);
  border-radius: 15px;
  margin-bottom: 20px;
  padding: 10px;
  display: flex;
 flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
}
.date{
  font-size: 12.5px;
  font-weight: bold;
}

.overlay{
  position:absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.77);
  display: flex;
  z-index: 10;
  align-items: center;
}

.modal{
  width:650px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
  margin: 0 auto;
}

.modal button{
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  color: white;
  border: none;
  margin-top: 15px;
  cursor: pointer;
}

.modal .close{
  background-color: red;
  margin-top: 7px;
  cursor: pointer;
}

.modal p{
  color: red;
  font-size: 12px;
  margin-top: 10px;
}
</style>
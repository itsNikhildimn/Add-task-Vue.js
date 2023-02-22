<script setup>
   import { ref } from 'vue';
   const showModel = ref(false)
   const newNote = ref("")
   const errorMsg = ref("")
   const notes = ref([])

   function getRandomColor() {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
   }

   const addNote= ()=> {
    if (newNote.value.length < 10){
     return errorMsg.value = "Atleast ten cheractors"
    }
    notes.value.push({
      id: Math.floor(Math.random() * 10000),
      text: newNote.value,
      date: new Date(),
      bgcolors: getRandomColor()
    })
    showModel.value = false;
    newNote.value=""
  }
</script>



<template>
  <main>
    <div v-if="showModel" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if = "errorMsg"> {{ errorMsg }}</p>
        <button @click="addNote">Add Note</button>
        <button  class="close" @click="showModel = false">Close</button>
      </div>
    </div>

      <div class="container">
        <header>
          <h1>Notes</h1>
          <button @click="showModel = true">+</button>
        </header>
        <div class="cards-container">
          <div v-for ="note in notes" :key="note.id" class="card" :style="{backgroundColor:note.bgcolors}">
            <p class="main-text">
              {{ note.text }}
            </p>
            <p class="date">
                 {{ note.date.toLocaleDateString("en-US") }}
            </p>
          </div>
        </div>
      </div>

  </main>
</template>



<style scoped>
main{
  height: 100%;
  width: 100%;
}
.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}
header{
  display: flex;
  align-items: center;
  justify-content: space-between;
}
h1{
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}
header button{
  border: none;
  cursor: pointer;
  height: 50px;
  width: 50px;
  border-radius: 50%;
  background-color: black;
  color: white;
  font-size: 20px;
}
.cards-container{
  display: flex;
  flex-wrap:wrap ;
}
.card{
  width: 225px;
  height: 225px;
  background-color: rgb(238, 176, 95);
  padding: 15px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 0 20px 20px 0;
}
.date{
  font-size: 12px;
  font-weight: bold;
}
.overlay{
  display: none;
  position: absolute;
  width:98vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}


.modal{
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal button{
  padding: 10px 20px;
  font-size: 18px;
  width: 100%;
  background-color: rgb(22, 130, 167);
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
  font-weight: bold;
}
.modal .close{
background-color: rgb(214, 97, 97);
}
.modal p{
  color: red;
}
</style>
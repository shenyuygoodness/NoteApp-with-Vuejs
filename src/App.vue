<script setup>
  import{ref} from "vue";

  const showModel = ref(false)
  const newNote = ref("") // for a single state
  const errorMessage = ref("")
  const notes = ref([]); //for state arrays

  function getRandomColor() {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  }

  const addNote = () => {
    if (newNote.value.length < 10){
      return errorMessage.value = "Notes need to be 10 characters"
    }
    notes.value.push({
      id: Math.floor(Math.random()* 1000000),
      text: newNote.value,
      date: new Date(),
      backgroundColor: getRandomColor()
    });
    showModel.value = false;
    newNote.value = ""
    errorMessage.value =""
  }
</script>
<template>
  <main>
    <div v-if="showModel" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if ="errorMessage">{{errorMessage}}</p>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModel = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModel = true">+</button>
      </header>
        <div class="card-container">
          <div v-for="note in notes" :key="note.id" class="card" :style="{backgroundColor: note.backgroundColor}">
            <p class="main-text">{{note.text}}</p>
            <p class="date">{{note.date.toLocaleDateString("en-Us")}}</p>
          </div>
        </div>
       
     
    </div>
  </main>
</template>

<style scoped>
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
  align-items: center;
  justify-content: space-between;
}
h1{
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 50px;
}
button{
  border: none;
  padding: 1%;
  width: 5%;
  border-radius: 15px;
  background-color: gold;
  cursor: pointer;
  font-size: 20px;
}

.card{
  width: 225px;height: 225px;
  background-color: rgb(181, 124, 95);
  border-radius: 10px;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  margin: 0% 15px;
  color: black;
}
.date{
  font-size: 12.5px;
  font-weight: bold;
}
.card-container{
  display: flex;
  flex-wrap: wrap;
}
.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0,77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;

}
.modal{
  background-color: white;
  width: 750px;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal button{
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  border: none;
  cursor: pointer;
  color: white;
  background-color: blueviolet;
  margin-top: 15px;
}
.modal .close{
  background-color: rgb(193, 20, 20);
  margin: 7px;
}
.modal p{
  color: red;
}
</style>
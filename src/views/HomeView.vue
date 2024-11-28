<script setup>
import { onMounted, ref } from "vue";
import axios from 'axios';

const deleteNote = async (index) =>{
  try {
    const noteId = notes.value[index].id; // Obtém o ID da nota a ser deletada
    await axios.delete(`http://localhost:8000/notes/${noteId}`); // Envia a requisição DELETE
    notes.value.splice(index, 1); // Remove a nota do array local
  } catch (error) {
    console.error("Erro ao deletar a nota:", error);
  }
}

const pad = ref({
  title: '',
  content: '',
  created_at: ''
});

const notes = ref({});

  onMounted(async ()=>{
    await  axios.get('http://localhost:8000/notes').then(response => {
      notes.value = response.data;
     });
  });

  
</script>

<template>
  <main class="grid grid-cols-2 gap-4 p-2">
    <div v-for="(note, index) in notes" :key="index" class="border w-full p-3 rounded-lg shadow-md">
       <h2 class="text-xl font-bold">{{ note.title }}</h2>
       <p class="">
        {{ note.content }}
       </p>
       <router-link to="#" class="bg-gray-200 px-3 rounded-full text-sm">
        All
       </router-link>
    </div>
  </main>
</template>

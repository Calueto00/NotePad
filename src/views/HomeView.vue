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

  const handleNote = async ()=>{
    const lastId = ref(notes.value.length ? notes.value[notes.value.length -1].id : 0);
   console.log(lastId.value);
    const newNote = ref({
      id: lastId.value,
      title: pad.value.title,
      content: pad.value.content,
      created_at: new Date().toISOString()
    });
    try {
      await  axios.post('http://localhost:8000/notes', newNote.value).then(response =>{
        notes.value.push(response.data);
      });
    } catch (error) {
      console.log(error);
    }
  }
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

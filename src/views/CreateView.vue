<script setup>

import axios from "axios";
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const note = ref({
    title: "",
    content: "",
});


const handleNote = async ()=>{
    const newNote = ref({
      title: note.value.title,
      content: note.value.content,
      created_at: new Date().toISOString()
    });
    try {
      await  axios.post('http://localhost:8000/notes', newNote.value).then(response =>{
        notes.value.push(response.data);
      });

      note.value.title = '';
      note.value.content = '';

      router.push('/');
    } catch (error) {
      console.log(error);
    }
  }
</script>

<template>
    <router-link to="/" class="border shadow-sm px-2 py-1 mt-2">back</router-link>
    <form class="mt-4 h-[400px] space-y-4" @submit.prevent="handleNote">
        <input v-model="note.title" type="text" class="outline-none w-full" placeholder="Title">
        <textarea v-model="note.content" class="outline-none w-full mt-2 h-1/2" placeholder="Write here"></textarea>
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-6 rounded-lg">Save</button>
    </form>
</template>
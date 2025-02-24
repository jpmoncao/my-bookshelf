<script setup lang="ts">
import { defineEmits, reactive } from 'vue';
import { useToast } from 'vue-toastification';
import Field from './Field.vue';
import Comment from './Comment.vue';
import Rating from './Rating.vue';


const emit = defineEmits();

const toast = useToast();

const formData = reactive({
  name: '',
  description: '',
  rating: 0,
});

const submitForm = () => {
  const { name, description, rating } = formData;

  if (name.trim() === '')
    return toast.error('Nome do livro é obrigatório!');
  
  if (rating <= 0)
    return toast.error('Avaliação é obrigatória!');

  emit('book-added', { name, description, rating });

  toast.success('Adicionado com sucesso!');
};
</script>

<template>
  <form method="post" class="flex flex-col gap-4 mx-auto max-w-[600px]" @submit.prevent="submitForm">
    <Field title="Nome do Livro" name="name" v-model="formData.name" />
    <Comment title="Descrição" name="description" v-model="formData.description" />
    <Rating v-model="formData.rating" />
    <div>
      <button class="bg-slate-700 px-4 py-1 rounded-sm text-white cursor-pointer hover:shadow-lg hover:scale-101 transition-all">Confirmar</button>
    </div>
  </form>
</template>

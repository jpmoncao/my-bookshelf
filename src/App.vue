<script setup lang="ts">
  import { ref } from 'vue';
  import { Star } from 'lucide-vue-next';
  import BookForm from './components/BookForm/BookForm.vue'

  const books = ref([
    {name: 'Diário de um banana', description: 'Livro muito legal', rating: 5},
    {name: 'O Pequeno Príncipe', description: 'Livro bom', rating: 4},
    {name: 'O Hobbit', description: 'Livro paia', rating: 1},
  ])
  
  const addBook = (newBook: { name: string; description: string; rating: number }) => {
    books.value.push(newBook);
  };
</script>

<template>
    <header class="w-full h-16 bg-slate-700 p-2 flex items-center fixed -top-[1px] left-0 z-50">
      <h1 class="text-2xl text-slate-100">My Bookshelf</h1>
    </header>

    <main class="py-18 px-2">
      <BookForm @book-added="addBook" />

      <hr class="w-[100vw] -ml-2 my-4 opacity-25">

      <section class="flex flex-col gap-4 max-w-[800px] mx-auto">
        <h2 class="text-xl text-slate-700">Livros</h2>
        <ul class="flex flex-col gap-2">
          <li v-for="book in books" :key="book.name" class="bg-slate-100 p-2 rounded-md h-22">
            <h3 class="text-lg text-slate-800 font-bold">{{ book.name }}</h3>
            <p class="text-slate-800">{{ book.description }}</p>
            <div class="flex items-center gap-0.5">
              <Star 
                class="text-slate-700 size-4"
                v-for="i in 5" 
                :key="i" 
                :class="{ 'opacity-100': book.rating >= i, 'opacity-30': book.rating < i }" 
              />
            </div>
          </li>
        </ul>
      </section>
    </main>
</template>

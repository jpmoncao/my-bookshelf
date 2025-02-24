<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';
import { Star } from 'lucide-vue-next';

defineProps({
  modelValue: {
    type: Number,
    default: 0,
  }
});

const emit = defineEmits(['update:modelValue']);
</script>

<template>
  <main>
    <p>Avaliação do livro</p>
    <div class="flex gap-4 mt-1">
      <div v-for="i in 5" :key="i" class="flex">
        <label :for="'rating-' + i" class="cursor-pointer hover:scale-105 hover:shadow-lg transition-all">
          <Star class="size-5 opacity-15" v-show="modelValue < i" />
          <Star class="size-5" v-show="modelValue >= i" />
        </label>
        <input 
          type="radio" 
          :id="'rating-' + i" 
          :value="i" 
          class="hidden" 
          :checked="modelValue === i" 
          @change="$emit('update:modelValue', i)" 
        />
      </div>
    </div>
  </main>
</template>

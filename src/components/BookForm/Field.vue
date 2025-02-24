<script setup lang="ts">
defineProps({
  name: String,
  title: String,
  modelValue: String,
});

defineEmits(['update:modelValue']);
</script>

<template>
  <div class="flex flex-col justify-start">
    <label :for="name">{{ title }}</label>
    <input 
      class="w-full rounded-md border px-2 py-0.5" 
      type="text" 
      :id="name" 
      :name="name" 
      :value="modelValue" 
      @input="$emit('update:modelValue', ($event.target as HTMLInputElement).value)" 
    />
  </div>
</template>

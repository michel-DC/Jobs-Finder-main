<script setup>
import { defineProps } from 'vue';

defineProps({
  titre: {
    type: String,
    default: 'Devenez développeur Front-End',
  },
  soustitre: {
    type: String,
    default: 'Trouvez un emploi facilement et rapidement grace à Corvex.',
  },
});
</script>

<template>
  <section class="bg-indigo-700 py-20 mb-4 rounded-b-3xl bg-[url('src/assets/img/bg-gold-blue.jpg')] ">
    <div
      class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col items-center"
    >
      <div class="text-center">
        <h1 class="text-4xl font-extrabold text-white sm:text-5xl md:text-6xl">
          {{ titre }}
        </h1>
        <p class="my-4 text-xl text-white">
          {{ soustitre }}
        </p>
      </div>
    </div>
  </section>
</template>

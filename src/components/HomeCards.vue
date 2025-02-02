<script setup>
import { RouterLink } from 'vue-router';
import Card from '@/components/Card.vue'; 
</script>

<template>
  <section class="py-4">
    <div class="container-xl lg:container m-auto">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-4 rounded-lg">
        <Card>
          <h2 class="text-2xl font-bold">Chercher un emploi</h2>
          <p class="mt-2 mb-4">
            Découvrez nos offres d'emploi pour devenir développeur Front-End et commencez votre carrière dès aujourd'hui.
          </p>
          <br>
          <RouterLink
            to="/jobs"
            class="inline-block bg-black text-white rounded-lg px-4 py-2 hover:bg-gray-700"
          >
            Voir tout les emplois
          </RouterLink>
        </Card>
        <Card bg="bg-indigo-100">
          <h2 class="text-2xl font-bold">Ajouter un nouvel emploi</h2>
          <p class="mt-2 mb-4">
            Vous êtes un recruteur en recherche d'un développeur Front-End talentueux ? Ajoutez une nouvelle offre d'emploi et trouvez le candidat idéal.
          </p>
          <RouterLink
            to="/jobs/add"
            class="inline-block bg-indigo-500 text-white rounded-lg px-4 py-2 hover:bg-indigo-600"
          >
            Ajouter un emploi
          </RouterLink>
        </Card>
      </div>
    </div>
  </section>
</template>

<script setup>
import Footer from '@/components/Footer.vue';
import { RouterLink } from 'vue-router';
import JobListing from '@/components/JobListing.vue';
import { reactive, defineProps, onMounted } from 'vue';
import PulseLoader from 'vue-spinner/src/PulseLoader.vue';
import axios from 'axios';
import { ref } from 'vue';

defineProps({
  limit: Number,
  showButton: {
    type: Boolean,
    default: false,
  },
});

const state = reactive({
  jobs: [],
  isLoading: true,
});

const message = ref(null);

const sendApplication = () => {
  message.value = "L'application pour ce métier a bien été envoyée.";
  setTimeout(() => {
    message.value = null; // Supprime le message après 3 secondes
  }, 3000);
};

onMounted(async () => {
  try {
    const response = await axios.get('/api/jobs');
    state.jobs = response.data;
  } catch (error) {
    console.error('Error fetching jobs', error);
  } finally {
    state.isLoading = false;
  }
});

const featuredJobs = [
  {
    id: 1,
    type: 'Temps plein',
    title: 'Développeur React.js',
    description: 'Créez des interfaces utilisateur à l`aide de React.js et des technologies Web modernes. Une solide connaissance de JavaScript, des hooks et de Redux est requise.',
    salary: '80,000€',
    location: 'Paris, France',
  },
  {
    id: 2,
    type: 'Temps partiel',
    title: 'Développeur Vue.js',
    description: 'Développez des composants front-end dynamiques avec Vue.js. Une expérience avec Vue Router, Vuex et Composition API est nécessaire.',
    salary: '70,000€',
    location: 'Télétravail',
  },
  {
    id: 3,
    type: 'Contrat',
    title: 'Développeur Angular',
    description: 'Proposez des applications frontales évolutives à l`aide d`Angular. Une expertise en TypeScript, RxJS et en gestion d`état est indispensable.',
    salary: '75,000 €',
    location: 'Lille, France',
  },
  {
    id: 4,
    type: 'Freelance',
    title: 'Dévéloppeur/Designer Front-End',
    description: 'Créez des conceptions réactives et intégrez-les dans un framework front-end. La maîtrise de HTML, CSS, JavaScript et Figma est essentielle.',
    salary: '65,000 €',
    location: 'Lyon, France',
  },
  {
    id: 5,
    type: 'Stage',
    title: 'Stagiaire Front-End',
    description: 'Participez à la création de projets front-end en collaboration avec une équipe expérimentée. Connaissance de base de HTML, CSS et JavaScript nécessaire.',
    salary: '1,000 €/mois',
    location: 'Marseille, France',
  },
  {
    id: 6,
    type: 'Temps plein',
    title: 'Développeur Next.js',
    description: 'Construisez des applications Web performantes en utilisant Next.js. Une expertise en SSR, ISR et API REST est essentielle.',
    salary: '85,000 €',
    location: 'Bordeaux, France',
  },
  {
    id: 7,
    type: 'Temps plein',
    title: 'Développeur Svelte',
    description: 'Implémentez des interfaces front-end modernes et rapides avec Svelte. Connaissance de transitions animées et stores est nécessaire.',
    salary: '78,000 €',
    location: 'Télétravail',
  },
  {
    id: 8,
    type: 'Contrat',
    title: 'Intégrateur Web',
    description: 'Convertissez des designs en pages Web interactives et accessibles. Une expertise en HTML5, CSS3 et frameworks CSS est essentielle.',
    salary: '60,000 €',
    location: 'Nantes, France',
  },
  {
    id: 9,
    type: 'Temps partiel',
    title: 'Développeur WordPress',
    description: 'Développez des sites Web personnalisés avec WordPress, en créant des thèmes et plugins sur mesure.',
    salary: '55,000 €',
    location: 'Nice, France',
  },
  {
    id: 10,
    type: 'Temps plein',
    title: 'Développeur Shopify',
    description: 'Créez et personnalisez des boutiques Shopify, avec une expertise en Liquid, JavaScript et intégration d`API.',
    salary: '72,000 €',
    location: 'Toulouse, France',
  },
  {
    id: 11,
    type: 'Freelance',
    title: 'Développeur Front-End Freelance',
    description: 'Travaillez avec des clients pour fournir des solutions frontales sur mesure. Bonne connaissance des frameworks modernes requise.',
    salary: '85,000 €',
    location: 'Télétravail',
  },
  {
    id: 12,
    type: 'Stage',
    title: 'Stagiaire Angular',
    description: 'Contribuez au développement de projets Angular en apprenant aux côtés de développeurs seniors.',
    salary: '1,200 €/mois',
    location: 'Strasbourg, France',
  },
  {
    id: 13,
    type: 'Temps plein',
    title: 'Développeur Front-End',
    description: 'Travaillez avec une équipe agile pour construire des interfaces interactives en utilisant les meilleures pratiques.',
    salary: '77,000 €',
    location: 'Grenoble, France',
  },
  {
    id: 14,
    type: 'Temps partiel',
    title: 'Développeur React Native',
    description: 'Créez des applications mobiles performantes en utilisant React Native. Expertise en Redux et intégration d`API requise.',
    salary: '68,000 €',
    location: 'Télétravail',
  },
  {
    id: 15,
    type: 'Contrat',
    title: 'Développeur UI/UX',
    description: 'Combinez design et développement pour offrir des expériences utilisateurs fluides et engageantes.',
    salary: '82,000 €',
    location: 'Lyon, France',
  },
  {
    id: 16,
    type: 'Freelance',
    title: 'Expert JavaScript Front-End',
    description: 'Fournissez des solutions innovantes en JavaScript pur ou frameworks modernes. Expérience avancée requise.',
    salary: '90,000 €',
    location: 'Télétravail',
  },
];

</script>

<template>
<section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-5xl font-bold text-indigo-500 mb-6 text-center">
        Liste des emplois disponibles
      </h2>
      <!-- Show loading spinner while loading is true -->
      <div v-if="state.isLoading" class="text-center text-gray-500 py-6">
        <PulseLoader />
      </div>

      <!-- Show job listing when done loading -->
      <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <JobListing
          v-for="job in state.jobs.slice(0, limit || state.jobs.length)"
          :key="job.id"
          :job="job"
        />
      </div>
    </div>
  </section>

  <!-- Featured jobs section -->
  <section class="bg-white py-10">
    <div class="container m-auto grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
      <div
        v-for="job in featuredJobs"
        :key="job.id"
        class="bg-white rounded-xl shadow-md relative p-4"
      >
        <div class="mb-6">
          <div class="text-gray-600 my-2">{{ job.type }}</div>
          <h3 class="text-xl font-bold">{{ job.title }}</h3>
        </div>

        <div class="mb-5">
          <div>
            {{ job.description.length > 90 ? job.description.substring(0, 90) + '...' : job.description }}
          </div>
        </div>

        <h3 class="text-green-500 mb-2">{{ job.salary }} / An</h3>

        <div class="border border-gray-100 mb-5"></div>

        <div class="flex flex-col lg:flex-row justify-between">
          <div class="text-orange-700">
            <i class="pi pi-map-marker text-orange-700"></i>
            {{ job.location }}
          </div>
          <!-- Application button -->
          <button
            @click="sendApplication"
            class="bg-indigo-500 rounded-lg font-medium w-28 justify-center text-lg text-white hover:bg-indigo-700"
          >
            Postuler
          </button>
        </div>
      </div>
    </div>
  </section>

  <!-- Confirmation message -->
  <div v-if="message" class="fixed bottom-10 right-10 bg-green-500 text-white py-3 px-6 rounded-lg shadow-lg">
    {{ message }}
  </div>
  <Footer />
</template>

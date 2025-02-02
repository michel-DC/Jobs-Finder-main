<script setup>
import router from '@/router';
import { reactive, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import { useToast } from 'vue-toastification';
import axios from 'axios';

const route = useRoute();

const jobId = route.params.id;

const form = reactive({
  type: 'Full-Time',
  title: '',
  description: '',
  salary: '',
  location: '',
  company: {
    name: '',
    description: '',
    contactEmail: '',
    contactPhone: '',
  },
});

const state = reactive({
  job: {},
  isLoading: true,
});

const toast = useToast();

const handleSubmit = async () => {
  const updatedJob = {
    title: form.title,
    type: form.type,
    location: form.location,
    description: form.description,
    salary: form.salary,
    company: {
      name: form.company.name,
      description: form.company.description,
      contactEmail: form.company.contactEmail,
      contactPhone: form.company.contactPhone,
    },
  };

  try {
    const response = await axios.put(`/api/jobs/${jobId}`, updatedJob);
    toast.success('Job Updated Successfully');
    router.push(`/jobs/${response.data.id}`);
  } catch (error) {
    console.error('Error fetching job', error);
    toast.error('Job Was Not Added');
  }
};

onMounted(async () => {
  try {
    const response = await axios.get(`/api/jobs/${jobId}`);
    state.job = response.data;
    // Populate inputs
    form.type = state.job.type;
    form.title = state.job.title;
    form.description = state.job.description;
    form.salary = state.job.salary;
    form.location = state.job.location;
    form.company.name = state.job.company.name;
    form.company.description = state.job.company.description;
    form.company.contactEmail = state.job.company.contactEmail;
    form.company.contactPhone = state.job.company.contactPhone;
  } catch (error) {
    console.error('Error fetching job', error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <section class="bg-indigo-50">
    <div class="container m-auto max-w-2xl py-24">
      <div class="bg-white px-6 py-8 mb-4 shadow-md rounded-md border m-4 md:m-0">
        <form @submit.prevent="handleSubmit">
          <h2 class="text-4xl font-bold text-center font-semibold mb-6">Modifier un emploi</h2>

          <div class="mb-4">
            <label for="type" class="block text-gray-700 font-bold mb-2">Type d'emploi</label>
            <select
              v-model="form.type"
              id="type"
              name="type"
              class="border rounded w-full py-2 px-3"
              required
            >
              <option value="Full-Time">Temps plein</option>
              <option value="Part-Time">Temps partiel</option>
              <option value="Remote">Télétravail</option>
              <option value="Internship">Stage</option>
            </select>
          </div>

          <div class="mb-4">
            <label for="title" class="block text-gray-700 font-bold mb-2">Nom de l'offre d'emploi</label>
            <input
              type="text"
              v-model="form.title"
              id="title"
              name="title"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="Ex: Développeur Front-End"
              required
            />
          </div>

          <div class="mb-4">
            <label for="description" class="block text-gray-700 font-bold mb-2">Description</label>
            <textarea
              id="description"
              v-model="form.description"
              name="description"
              class="border rounded w-full py-2 px-3"
              rows="4"
              placeholder="Ajoutez des détails sur l'emploi : tâches, attentes, exigences, etc."
              required
            ></textarea>
          </div>

          <div class="mb-4">
            <label for="salary" class="block text-gray-700 font-bold mb-2">Salaire</label>
            <select
              id="salary"
              v-model="form.salary"
              name="salary"
              class="border rounded w-full py-2 px-3"
            >
              <option value="Under $50K">Moins de 50K €</option>
              <option value="$50K - $60K">50 - 60K €</option>
              <option value="$60K - $70K">60 - 70K €</option>
              <option value="$70K - $80K">70 - 80K €</option>
              <option value="$80K - $90K">80 - 90K €</option>
              <option value="$90K - $100K">90 - 100K €</option>
              <option value="$100K - $125K">100 - 125K €</option>
              <option value="$125K - $150K">125 - 150K €</option>
              <option value="$150K - $175K">150 - 175K €</option>
              <option value="$175K - $200K">175 - 200K €</option>
              <option value="Over $200K">Plus de 200K €</option>
            </select>
          </div>

          <div class="mb-4">
            <label for="location" class="block text-gray-700 font-bold mb-2">Localisation</label>
            <input
              type="text"
              v-model="form.location"
              id="location"
              name="location"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="Où se situe l'emploi ?"
              required
            />
          </div>

          <h3 class="text-2xl mb-5">Informations sur votre entreprise</h3>

          <div class="mb-4">
            <label for="company" class="block text-gray-700 font-bold mb-2">Nom de votre entreprise</label>
            <input
              type="text"
              v-model="form.company.name"
              id="company"
              name="company"
              class="border rounded w-full py-2 px-3"
              placeholder="Ex: Google"
            />
          </div>

          <div class="mb-4">
            <label for="company_description" class="block text-gray-700 font-bold mb-2">
              Description de l'entreprise
            </label>
            <textarea
              id="company_description"
              v-model="form.company.description"
              name="company_description"
              class="border rounded w-full py-2 px-3"
              rows="4"
              placeholder="Que faites-vous ?"
            ></textarea>
          </div>

          <div class="mb-4">
            <label for="contact_email" class="block text-gray-700 font-bold mb-2">Adresse e-mail</label>
            <input
              type="email"
              v-model="form.company.contactEmail"
              id="contact_email"
              name="contact_email"
              class="border rounded w-full py-2 px-3"
              placeholder="Adresse e-mail pour les candidatures"
              required
            />
          </div>

          <div class="mb-4">
            <label for="contact_phone" class="block text-gray-700 font-bold mb-2">Numéro de téléphone</label>
            <input
              type="tel"
              v-model="form.company.contactPhone"
              id="contact_phone"
              name="contact_phone"
              class="border rounded w-full py-2 px-3"
              placeholder="Numéro de téléphone pour les candidatures"
            />
          </div>

          <div>
            <button
              class="bg-indigo-500 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline"
              type="submit"
            >
              Ajouter cet emploi
            </button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>
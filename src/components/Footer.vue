<script setup>
import { ref } from 'vue';

const currentYear = new Date().getFullYear();
const currentDay = ref(new Date().getDay());

const socialLinks = [
  { name: 'Facebook', icon: 'pi pi-facebook', url: 'https://facebook.com' },
  { name: 'Twitter', icon: 'pi pi-twitter', url: 'https://twitter.com' },
  { name: 'LinkedIn', icon: 'pi pi-linkedin', url: 'https://linkedin.com' },
  { name: 'Instagram', icon: 'pi pi-instagram', url: 'https://instagram.com' },
];
</script>

<template>
  <footer class="bg-gradient-to-r from-blue-500 via-orange-400 to-black h-full text-white py-10">
    <div class="container m-auto max-w-6xl px-6 lg:px-12">
      <!-- Footer Top Section -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <!-- Navigation Links -->
        <div>
          <h3 class="font-bold text-xl mb-4">Navigation rapide</h3>
          <ul class="space-y-2">
            <li><router-link to="/" class="hover:underline">Accueil</router-link></li>
            <li><router-link to="/about" class="hover:underline">À propos</router-link></li>
            <li><router-link to="/jobs" class="hover:underline">Emplois</router-link></li>
            <li><router-link to="/contact" class="hover:underline">Contact</router-link></li>
          </ul>
        </div>

        <!-- Contact Information -->
        <div>
          <h3 class="font-bold text-xl mb-4">Contact</h3>
          <p class="mb-2">123 Rue de l'Innovation, Paris</p>
          <p class="mb-2">Email: <a href="mailto:info@monsite.com" class="underline">info@corvex.com</a></p>
          <p>Téléphone: <a href="tel:+33123456789" class="underline">+33 1 23 45 67 89</a></p>
        </div>

        <!-- Social Links -->
        <div>
          <h3 class="font-bold text-xl mb-4">Suivez-nous</h3>
          <ul class="flex space-x-4">
            <li v-for="link in socialLinks" :key="link.name">
              <a
                :href="link.url"
                target="_blank"
                rel="noopener noreferrer"
                class="hover:text-gray-300 text-2xl"
              >
                <i :class="link.icon"></i>
              </a>
            </li>
          </ul>
        </div>
      </div>

      <!-- Footer Bottom Section -->
      <div class="border-t border-indigo-400 mt-8 pt-6 text-center text-sm">
        <p>&copy; {{ currentYear }} Corvex. Tous droits réservés.</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
footer {
  font-family: 'Inter', sans-serif;
}

a {
  text-decoration: none;
  color: inherit;
}
</style>

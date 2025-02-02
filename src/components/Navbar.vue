<script setup>
import { RouterLink, useRoute } from 'vue-router';
import logo from '@/assets/img/icon-top.png';

const isActiveLink = (routePath) => {
  const route = useRoute();
  return route.path === routePath;
};
</script>

<template>
  <nav class="bg-black border-b border-black-xs">
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
      <div class="flex h-20 items-center justify-between">
        <div
          class="flex flex-1 items-center justify-center md:items-stretch md:justify-start"
        >
          <!-- Logo -->
          <RouterLink class="flex flex-shrink-0 items-center mr-4" to="/">
            <img class="h-10 w-auto" :src="logo" alt="Vue Jobs" />
            <span class="hidden md:block text-white text-2xl font-bold ml-2"
              >Corvex</span
            >
          </RouterLink>
          <div class="md:ml-auto">
            <div class="flex space-x-2">
              <RouterLink
                to="/"
                :class="[
                  isActiveLink('/')
                    ? 'bg-indigo-900 rounded-2xl'
                    : 'hover:bg-gray-900 hover:text-white rounded-2xl',
                  'text-white',
                  'px-3',
                  'py-2',
                  'rounded-md',
                ]"
                >Home</RouterLink
              >
              <RouterLink
                to="/jobs"
                :class="[
                  isActiveLink('/jobs')
                    ? 'bg-indigo-900 rounded-2xl'
                    : 'hover:bg-gray-900 hover:text-white rounded-2xl',
                  'text-white',
                  'px-3',
                  'py-2',
                  'rounded-md',
                ]"
                >Trouver un emploi</RouterLink
              >
              <RouterLink
                to="/jobs/add"
                :class="[
                  isActiveLink('/jobs/add')
                    ? 'bg-indigo-900 rounded-2xl'
                    : 'hover:bg-gray-900 hover:text-white rounded-2xl',
                  'text-white',
                  'px-3',
                  'py-2',
                  'rounded-md',
                ]"
                >Ajouter un emploi</RouterLink
              >
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

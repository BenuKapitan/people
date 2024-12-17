<script setup lang="ts">
import PeopleCard from '@/components/PeopleCard.vue';
import data_people from '@/data/data_people';
import type People from '@/types/People';
import { ref } from 'vue';

const people = ref<People[]>(data_people.getPeople());
const sortOrder = ref<'asc' | 'desc'>('asc');

const sortPeople = () => {
  people.value.sort((a, b) => {
    const nameA = `${a.first_name} ${a.last_name}`.toLowerCase();
    const nameB = `${b.first_name} ${b.last_name}`.toLowerCase();
    if (sortOrder.value === 'asc') {
      return nameA.localeCompare(nameB);
    } else {
      return nameB.localeCompare(nameA);
    }
  });
};

const toggleSortOrder = () => {
  sortOrder.value = sortOrder.value === 'asc' ? 'desc' : 'asc';
  sortPeople();
};

sortPeople();
</script>

<template>
  <h1 class="display-5">Emberek</h1>
  <button @click="toggleSortOrder">
    Sort {{ sortOrder === 'asc' ? 'A-Z' : 'Z-A' }}
  </button>
  <div>
    <PeopleCard v-for="person in people" :key="person.id" :person="person" />
  </div>
</template>

<style scoped>
/* Add any necessary styles here */
</style>
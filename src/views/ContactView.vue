<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import data_people from '@/data/data_people';
import type People from '@/types/People';

const route = useRoute();
const router = useRouter();
const person = ref<People | null>(null);

onMounted(() => {
  const personId = Number(route.params.id);
  person.value = data_people.getPeople().find(p => p.id === personId) || null;
});

const goBack = () => {
  router.back();
};
</script>

<template>
  <div id="PeopleCard" v-if="person">
    <img id="profilePic" :src="person.avatar" :alt="`${person.first_name} ${person.last_name}`" />
    <h1 id="Name">{{ person.first_name }} {{ person.last_name }}</h1>
    <p id="email">{{ person.email }}</p>
    <button @click="goBack">Back</button>
  </div>
  <div v-else>
    <p>Person not found</p>
  </div>
</template>

<style scoped>
.peopleCard {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1em;
  border: 1px solid #ccc;
  border-radius: 5px;
  cursor: pointer;
}
.profilePic {
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
.Name {
  font-size: 1.5em;
  font-weight: bold;
}
.Email {
  font-size: 1em;
}
</style>
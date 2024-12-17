<script setup lang="ts">
import { useRouter } from 'vue-router';
import type People from '@/types/People';

interface Props {
  person: People;
}

const props = defineProps<Props>();
const router = useRouter();

const navigateToContact = () => {
  router.push(`/contact/${props.person.id}`);
};
</script>

<template>
  <div id="peopleCard" @click="navigateToContact">
    <img id="profilePic" :src="person.avatar" :alt="`${person.first_name} ${person.last_name}`" />
    <h2 id="name"> {{ person.first_name }} {{ person.last_name }}</h2>
    <p id="email">{{ person.email }}</p>
  </div>
</template>

<style scoped>
#peopleCard {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1.5em;
  border: 1px solid #ddd;
  border-radius: 10px;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
  background-color: #f9f9f9;
}

#peopleCard:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

#profilePic {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  margin-bottom: 1em;
}

#name {
  font-size: 1.6em;
  font-weight: bold;
  margin: 0.5em 0;
  color: #333;
}

#email {
  font-size: 1em;
  color: #666;
}
</style>
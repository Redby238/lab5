<template>
  <div :class="cardClass">
    <img :src="userData.photo" alt="User Photo" />
    <h2>{{ userData.firstName }} {{ userData.lastName }}</h2>
    <p>{{ userData.gender }}</p>
    <p v-if="userData.age > 18">{{ userData.age }} років</p>
    <p>{{ userData.position }}</p>
    <ul>
      <li v-for="hobby in userData.hobbies" :key="hobby">{{ hobby }}</li>
    </ul>
  </div>
</template>

<script lang="ts" setup>
import { computed, defineProps } from 'vue';

interface UserData {
  firstName: string;
  lastName: string;
  gender: string;
  age: number;
  position: string;
  photo: string;
  hobbies: string[];
}

const props = defineProps<{ userData: UserData }>();

const cardClass = computed(() => {
  return props.userData.age > 18 ? 'card-adult' : 'card-young';
});
</script>

<style scoped>
.card-adult {
  background-color: lightblue;
}
.card-young {
  background-color: lightgreen;
}
img {
  width: 150px;
  height: 150px;
  border-radius: 50%;
}
div {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px;
  border-radius: 8px;
}
h2 {
  font-size: 1.5rem;
}
ul {
  list-style-type: none;
  padding: 0;
}
</style>

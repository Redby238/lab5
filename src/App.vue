<template>
  <div>
    <div class="toolbar">
      <button @click="filterUsers('Чоловік')">Чоловік</button>
      <button @click="filterUsers('Жінка')">Жінка</button>
      <button @click="clearFilter">Показати всіх</button>
    </div>

    <div v-if="filteredUsers.length === 0">Список користувачів порожній</div>
    <div v-else>
      <UserCard v-for="user in filteredUsers" :key="user.firstName" :userData="user" />
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from 'vue';
import UserCard from './components/UserCard.vue';

interface UserData {
  firstName: string;
  lastName: string;
  gender: string;
  age: number;
  position: string;
  photo: string;
  hobbies: string[];
}

const users: UserData[] = [
  { firstName: 'Іван', lastName: 'Петренко', gender: 'Чоловік', age: 25, position: 'Розробник', photo: new URL('@/assets/images/1.jpg', import.meta.url).href, hobbies: ['Читання', 'Програмування', 'Піші прогулянки'] },
  { firstName: 'Марія', lastName: 'Коваль', gender: 'Жінка', age: 30, position: 'Дизайнер', photo: new URL('@/assets/images/6.jpg', import.meta.url).href, hobbies: ['Малювання', 'Співи', 'Подорожі'] },
  { firstName: 'Олексій', lastName: 'Сидоренко', gender: 'Чоловік', age: 22, position: 'Менеджер', photo: new URL('@/assets/images/2.jpg', import.meta.url).href, hobbies: ['Ігри', 'Футбол'] },
  { firstName: 'Олена', lastName: 'Гриценко', gender: 'Жінка', age: 27, position: 'Художник', photo: new URL('@/assets/images/7.jpg', import.meta.url).href, hobbies: ['Малювання', 'Фотографія'] },
  { firstName: 'Михайло', lastName: 'Кравченко', gender: 'Чоловік', age: 21, position: 'Письменник', photo: new URL('@/assets/images/3.jpg', import.meta.url).href, hobbies: ['Письмо', 'Блогінг'] },
  { firstName: 'Анастасія', lastName: 'Бойко', gender: 'Жінка', age: 19, position: 'Музикант', photo: new URL('@/assets/images/8.jpg', import.meta.url).href, hobbies: ['Гра на гітарі', 'Співи'] },
  { firstName: 'Дмитро', lastName: 'Мельник', gender: 'Чоловік', age: 32, position: 'Шеф-кухар', photo: new URL('@/assets/images/4.jpg', import.meta.url).href, hobbies: ['Кулінарія', 'Подорожі'] },
  { firstName: 'Софія', lastName: 'Лисенко', gender: 'Жінка', age: 18, position: 'Студентка', photo: new URL('@/assets/images/9.jpg', import.meta.url).href, hobbies: ['Танці', 'Читання'] },
  { firstName: 'Андрій', lastName: 'Захаренко', gender: 'Чоловік', age: 26, position: 'Інженер', photo: new URL('@/assets/images/5.jpg', import.meta.url).href, hobbies: ['Робототехніка', 'Піші прогулянки'] },
  { firstName: 'Катерина', lastName: 'Дорошенко', gender: 'Жінка', age: 28, position: 'Лікар', photo: new URL('@/assets/images/10.jpg', import.meta.url).href, hobbies: ['Медицина', 'Біг'] }
];


const selectedGender = ref('');

const filteredUsers = computed(() => {
  if (!selectedGender.value) return users;
  return users.filter(user => user.gender === selectedGender.value);
});

function filterUsers(gender: string) {
  selectedGender.value = gender;
}

function clearFilter() {
  selectedGender.value = '';
}
</script>

<style scoped>
.toolbar {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

button {
  padding: 10px;
  font-size: 1rem;
  cursor: pointer;
}

button:hover {
  background-color: #ddd;
}
</style>

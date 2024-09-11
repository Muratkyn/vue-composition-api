<template>
  <section class="container">
    <h2>{{ user }}</h2>
    <h3>{{ age }}</h3>
    <p v-if="isVisible">Changed!</p>
    <button @click="changeAge">Change</button>
    <!-- <h2>{{ user1.name }}</h2> -->
    <div>
      <input type="text" placeholder="First name" v-model="user2.firstName" />
      <input type="text" placeholder="Last name" v-model="user2.lastName" />
    </div>
  </section>
</template>

<script setup>
import { ref, computed, watch, reactive } from 'vue';
//import 'reactive' which is a bit like ref but explicilty for objects
// const user1 = reactive({
//   name: 'Murat',
//   age: 30,
// });

const age = ref(30);
const isVisible = ref(false);
const user2 = reactive({
  firstName: '',
  lastName: '',
});

// computed is Readonly!
const user = computed(() => {
  return `${user2.firstName} ${user2.lastName}`;
});

watch([age, user, user2.lastName], (newVals, oldVals) => {
  console.log(oldVals[0], 'old value');
  console.log(newVals[0], 'new value');
  console.log(oldVals[1], 'old full name');
  console.log(newVals[1], 'old full name');
});

function changeAge() {
  age.value = 3;
  isVisible.value = true;
  setTimeout(() => {
    isVisible.value = false;
    // user1.name = 'Murati';
  }, 2000);
}
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>

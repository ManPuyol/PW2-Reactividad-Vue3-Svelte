<template>
  <div>
    <h1>Ref</h1>
    <div class="box">
      <p>Valor de count: <b>{{ count }}</b></p>
      <button @click="increment">+1</button>
    </div>

    <h1>Reactive</h1>
    <div class="box">
      <p>Nombre: <b>{{ user.name }}</b><br>
      Edad: <b>{{ user.age }}</b></p>
      <button @click="toggleUser">Alternar</button>
    </div>

    <h1>Computed</h1>
    <div class="box">
      <p>Nombre completo: <b>{{ fullName }}</b></p>
      <input v-model="firstName" placeholder="Nombre">
      <input v-model="lastName" placeholder="Apellido">
    </div>

    <h1>Watch</h1>
    <div class="box">
      <p>Edad actual: <b>{{ age }}</b></p>
      <input v-model="newAge" placeholder="Nueva edad">
    </div>
  </div>
</template>

<script>
import { ref, reactive, computed, watch } from 'vue';

export default {
  setup() {
    const count = ref(0);
    function increment() {
      count.value++;
    }

    const initialUser = { name: 'Juan', age: 25 };
    const updatedUser = { name: 'Pedro', age: 30 };
    /*
    Es necesario {...initialUser} para pasar una copia del objeto en este caso. 
    Sino entonces la variable initialUser se volvera reactiva cambiara su valor
    */
    const user = reactive({...initialUser});
    let isInitial = true;

    function toggleUser() {
      user.name = isInitial ? updatedUser.name : initialUser.name;
      user.age = isInitial ? updatedUser.age : initialUser.age;
      isInitial = !isInitial;
      console.log(user, isInitial, updatedUser, initialUser)
    }

    const firstName = ref('');
    const lastName = ref('');

    const fullName = computed(() => {
      return `${firstName.value} ${lastName.value}`;
    });

    const age = ref(20);
    const newAge = ref('');


    watch(newAge, (value) => {
      if (!isNaN(value)) {
        age.value = parseInt(value) | 0;
      }
    });

    return {
      count,
      increment,
      user,
      toggleUser,
      firstName,
      lastName,
      fullName,
      age,
      newAge,
    };
  }
}
</script>

<style>

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.box {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: linear-gradient(315deg,#42d392 25%,#647eff);
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 8px;
  color: #fff;
}

input {
  margin-top: 10px;
  padding: 8px;
  border: none;
  border-radius: 4px;
  outline: none;
  width: max-content;
}

button {
  width: max-content;
  padding: 10px 20px;
  background-color: #2d4059;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #1b262c;
}
</style>

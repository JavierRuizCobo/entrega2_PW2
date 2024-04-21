<template>
    <div>
      <h1>Lista de Usuarios con reactive</h1>
      <ul>
        <li v-for="user in users" :key="user.id">
          {{ user.name }} - {{ user.email }}
          <button @click="removeUser(user.id)">Eliminar</button>
        </li>
      </ul>
      <div class="user-form">
        <input type="text" v-model="newUser.name" placeholder="Nombre">
        <input type="email" v-model="newUser.email" placeholder="Correo electrónico">
        <button @click="addUser">Agregar Usuario</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { reactive } from 'vue';
  
  const users = reactive([
    { id: 1, name: "Javier Ruiz", email: "javier@ruiz.com" },
    { id: 2, name: "Manolito Gomez", email: "manolito@gomez.com" },
  ]);
  
  const newUser = reactive({
    name: "",
    email: "",
    });
  
  const addUser = () => {
    if (newUser.name && newUser.email) {
      const newUserId = Date.now();
      users.push({
        id: newUserId,
        name: newUser.name,
        email: newUser.email,
      });
      newUser.name = "";
      newUser.email = "";
    }
  };
  
  const removeUser = (userId) => {
    const userIndex = users.findIndex((user) => user.id === userId);
    if (userIndex !== -1) {
      users.splice(userIndex, 1);
    }
  };
  </script>
  
  <style scoped>
  .user-form {
    margin-top: 20px;
    display: flex;
    gap: 10px;
  }
  
  input[type="text"],
  input[type="email"] {
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  
  button {
    padding: 5px 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    cursor: pointer;
  }
  </style>
  
<template>
  <div class="box">
    <h1>PetHope 🐾</h1>
    <p>Quem é você?</p>

    <router-link to="/login">Pessoa Física</router-link>
    <router-link to="/login_ong">ONG</router-link>
  </div>
</template>

<script setup>
import '../styles/opcoes_login.css'
</script>

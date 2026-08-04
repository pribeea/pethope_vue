<template>
  <div>
    <h1>Solicitações de adoção</h1>

    <template v-if="solicitacoes.length">
      <div v-for="s in solicitacoes" :key="s.id">
        <hr />
        <h3>{{ s.animal.nome }}</h3>
        <p><strong>Interessado:</strong> {{ s.usuario.nome }}</p>
        <p><strong>Status:</strong> {{ s.status }}</p>

        <template v-if="s.status === 'Pendente'">
          <button type="button" @click="aprovar(s.id)">Aprovar</button>
          <button type="button" @click="recusar(s.id)">Recusar</button>
        </template>
        <p v-else-if="s.status === 'Aprovada'" style="color: green">✅ Solicitação aprovada.</p>
        <p v-else-if="s.status === 'Recusada'" style="color: red">❌ Solicitação recusada.</p>
      </div>
    </template>

    <p v-else>Nenhuma solicitação de adoção encontrada.</p>

    <br />
    <router-link to="/dashboard_ong" class="btn-voltar">Voltar</router-link>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import http from '../api/http'
import '../styles/solicitacoes.css'

const solicitacoes = ref([])

async function carregar() {
  const { data } = await http.get('/api/adoptions/requests')
  solicitacoes.value = data
}

async function aprovar(id) {
  await http.post(`/api/adoptions/${id}/approve`)
  carregar()
}

async function recusar(id) {
  await http.post(`/api/adoptions/${id}/reject`)
  carregar()
}

onMounted(carregar)
</script>

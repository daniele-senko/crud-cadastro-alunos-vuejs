<template>
  <div>
    <h1>Cadastro de Alunos</h1>
    <p>Total de alunos: {{ alunos.length }}</p>
    
    <button @click="mostrarForm = !mostrarForm">
      {{ mostrarForm ? 'Ocultar formulário' : 'Mostrar formulário' }}
    </button>

    <hr />

    <div v-show="mostrarForm">
      <h2 v-if="editandoId === null">Cadastrar</h2>
      <h2 v-else>Editar</h2>

      <div style="margin-bottom: 8px;">
        <label>Nome: <input v-model="nome" type="text" placeholder="Ex: Maria Souza" /></label>
      </div>
      <div style="margin-bottom: 8px;">
        <label>Matrícula: <input v-model="matricula" type="text" placeholder="Ex: 2026001" /></label>
      </div>
      <div style="margin-bottom: 8px;">
        <label>Curso: <input v-model="curso" type="text" placeholder="Ex: Sistemas de Informação" /></label>
      </div>
      <div style="margin-bottom: 8px;">
        <label>Ativo: <input v-model="ativo" type="checkbox" /></label>
      </div>

      <button style="margin-right: 8px;" @click="salvar">Salvar</button>
      <button @click="limpar">Cancelar</button>
    </div>

    <hr />

    <ul v-if="alunos.length > 0">
      <li v-for="(a, i) in alunos" :key="a.id" style="margin-bottom: 12px;">
        #{{ i + 1 }} — {{ a.nome }} | {{ a.matricula }} | {{ a.curso }} | {{ a.ativo ? 'Ativo' : 'Inativo' }}
        
        <button style="margin-left: 12px;" @click="editar(a)">Editar</button>
        <button style="margin-left: 4px;" @click="excluir(a.id)">Excluir</button>
      </li>
    </ul>
    
    <p v-else>Nenhum aluno cadastrado ainda. Cadastre o primeiro!</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'; // [cite: 127]

// Estado da lista e do formulário [cite: 128, 129, 130, 131]
const alunos = ref([]);
const mostrarForm = ref(false);

// Controle de edição (null = cadastrando novo, número = editando) [cite: 95, 96, 133, 134]
const editandoId = ref(null);

// Campos do formulário [cite: 135-142]
const nome = ref('');
const matricula = ref('');
const curso = ref('');
const ativo = ref(true);

// Funções base vazias (implementaremos a seguir) [cite: 143-147]
function salvar() {
  // Implementaremos no próximo passo
}

function editar(a) {
  // Implementaremos no próximo passo
}

function excluir(id) {
  // Implementaremos no próximo passo
}

function limpar() {
  // Implementaremos no próximo passo
}
</script>
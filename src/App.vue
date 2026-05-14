<template>
  <div>
    <h1>Cadastro de Alunos</h1>
    <p>Total de alunos: {{ alunos.length }}</p>

    <button @click="mostrarForm = !mostrarForm">
      {{ mostrarForm ? "Ocultar formulário" : "Mostrar formulário" }}
    </button>

    <hr />

    <div v-show="mostrarForm">
      <h2 v-if="editandoId === null">Cadastrar</h2>
      <h2 v-else>Editar</h2>

      <div style="margin-bottom: 8px">
        <label
          >Nome:
          <input v-model="nome" type="text" placeholder="Ex: Maria Souza"
        /></label>
      </div>
      <div style="margin-bottom: 8px">
        <label
          >Matrícula:
          <input v-model="matricula" type="text" placeholder="Ex: 2026001"
        /></label>
      </div>
      <div style="margin-bottom: 8px">
        <label
          >Curso:
          <input
            v-model="curso"
            type="text"
            placeholder="Ex: Sistemas de Informação"
        /></label>
      </div>
      <div style="margin-bottom: 8px">
        <label>Ativo: <input v-model="ativo" type="checkbox" /></label>
      </div>

      <button style="margin-right: 8px" @click="salvar">Salvar</button>
      <button @click="limpar">Cancelar</button>
    </div>

    <hr />

    <ul v-if="alunos.length > 0">
      <li v-for="(a, i) in alunos" :key="a.id" style="margin-bottom: 12px">
        #{{ i + 1 }} — {{ a.nome }} | {{ a.matricula }} | {{ a.curso }} |
        {{ a.ativo ? "Ativo" : "Inativo" }}

        <button style="margin-left: 12px" @click="editar(a)">Editar</button>
        <button style="margin-left: 4px" @click="excluir(a.id)">Excluir</button>
      </li>
    </ul>

    <p v-else>Nenhum aluno cadastrado ainda. Cadastre o primeiro!</p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const alunos = ref([]);
const mostrarForm = ref(false);
const editandoId = ref(null);
const nome = ref("");
const matricula = ref("");
const curso = ref("");
const ativo = ref(true);

function salvar() {
  if (editandoId.value === null) {
    const novoAluno = {
      id: Date.now(),
      nome: nome.value,
      matricula: matricula.value,
      curso: curso.value,
      ativo: ativo.value,
    };
    alunos.value.push(novoAluno);
  } else {
    const index = alunos.value.findIndex((a) => a.id === editandoId.value);

    if (index !== -1) {
      alunos.value[index].nome = nome.value;
      alunos.value[index].matricula = matricula.value;
      alunos.value[index].curso = curso.value;
      alunos.value[index].ativo = ativo.value;
    }
  }

  // Limpa os campos após salvar
  limpar();
}

function limpar() {
  nome.value = "";
  matricula.value = "";
  curso.value = "";
  ativo.value = true;
  editandoId.value = null;
}

function editar(a) {
  nome.value = a.nome;
  matricula.value = a.matricula;
  curso.value = a.curso;
  ativo.value = a.ativo;
  editandoId.value = a.id;
  mostrarForm.value = true;
}

function excluir(id) {
  alunos.value = alunos.value.filter((aluno) => aluno.id !== id);

  if (editandoId.value === id) {
    limpar();
  }
}
</script>

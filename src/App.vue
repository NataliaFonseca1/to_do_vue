<script setup>
import { reactive, transformVNodeArgs } from 'vue';

const estado = reactive({
  filtro:"todas",
  tarefaTemp:'',
  tarefas: [
  {
    titulo:"Estudar ES6",
    finalizada:false,
  },
  {
    titulo:"estudar Sass",
    finalizada:false,

  },
  {
    titulo:"Ir para academia", 
    finalizada:true,
  }
]
})
 const getTarefasPendentes = () =>{
 return estado.tarefas.filter(tarefas => !tarefas.finalizada)
 }
 const getTarefasFinalizadas = () =>{
 return estado.tarefas.filter(tarefas => tarefas.finalizada)
 }

 const getTarefasFiltradas =  () =>{
  const {filtro}= estado; /* desestruturação - variação:  filtro = estado.filtro*/
  switch (filtro){
    case 'pendentes':return getTarefasPendentes();
    case 'finalizadas': return getTarefasFinalizadas();
    default: 
    return estado.tarefas
  }
 }
const cadastraTarefa=() =>{
  const tarefaNova={
    titulo:estado.tarefaTemp,
    finalizada:false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp=" ";
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }}  tarefas pendentes
      </p>
    </header>

<form @submit.prevent="cadastraTarefa">
<div class="row">
  <div class="col">
    <input :value="estado.tarefaTemp" @change="evento=> estado.tarefaTemp = evento.target.value" required type="text" placehplder="digite aqui a descrição da tarefa" class="form-control">
  </div>
  <div class="col-md-1">
    <button type="submit" class="btn btn-primary">Cadastrar</button>
  </div>
  <div class="col-md-2">
    <select @change="evento => estado.filtro = evento.target.value" class="form-control">
      <option value="todas">todas tarefas</option>
      <option value="pendentes">pendentes</option>
      <option value="finalizadas">finalizadas</option>
    </select>
  </div>
</div>
</form>

<ul class="list-group mt-4">
  <li class="list-group-item" v-for="tarefas in getTarefasFiltradas()">
<input @change="evento => tarefas.finalizada=evento.target.checked" :checked="tarefas.finalizada" :id="tarefas.titulo" type="checkbox">
<label :class="{done:tarefas.finalizada === true }" :for="tarefas.titulo" class="ms-3">
  {{ tarefas.titulo }}</label>
  </li>
</ul>
</div>
</template>


<style scoped>
.done{
  text-decoration: line-through;
}
</style>

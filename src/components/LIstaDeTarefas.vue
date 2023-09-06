<script setup>
const props = defineProps(['tarefas']);

</script> 


<template>
<ul class="list-group mt-4">
  <li class="list-group-item" v-for="tarefas in props.tarefas">
<input @change="evento => tarefas.finalizada=evento.target.checked" :checked="tarefas.finalizada" :id="tarefas.titulo" type="checkbox">
<label :class="{done:tarefas.finalizada === true }" :for="tarefas.titulo" class="ms-3">
  {{ tarefas.titulo }}</label>
  </li>
</ul>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>

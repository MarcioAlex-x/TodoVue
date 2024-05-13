<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    tarefaTemp : '',
    filtro: 'todas',
    tarefas:[
    {
      titulo: 'Estudar VueJs',
      finalizada: true,
     },
     {
      titulo: 'Estudar React',
      finalizada: false
     },
     {
      titulo:'Estudar Java',
      finalizada: false
     }
    ]
  })

  const getTarefasPendentes = () =>{
    return estado.tarefas.filter((tarefa)=>{
      return !tarefa.finalizada
    })
  }
  const getTarefasFinalizadas = () =>{
    return estado.tarefas.filter((tarefa)=>{
      return tarefa.finalizada
    })
  }

  const getTarefasFiltradas = () =>{
    const { filtro } = estado

    switch(filtro){
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas()
      default:
        return estado.tarefas
    }
  }
  const cadastraTarefa = () =>{
    const novaTarefa = {
      titulo:estado.tarefaTemp,
      finalizada:false
    }
    estado.tarefas.push(novaTarefa)
    estado.tarefaTemp = ''
  }
</script>

<template>
  <div class="container">
    <header class="p-5 my-4 bg-light rounded-3">
    <h1>Tarefas</h1>
    <p>
      Você possui {{ getTarefasPendentes().length }} tarefas pendentes.
    </p>
  </header>
  <form @submit.prevent="cadastraTarefa">
    <div class="row">
      <div class="col">
        <input :value="estado.tarefaTemp" @change="e => estado.tarefaTemp = e.target.value" requiredtype="text" placeholder="Informe a nova tarefa!" class="form-control">
      </div>
      <div class="col-md-2">
        <button type="submit"class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select class="form-control"  @change="e => estado.filtro = e.target.value">
          <option value="todas">Todas as tarefas</option>
          <option value="pendentes">Tarefas pendentes</option>
          <option value="finalizadas">Tarefas finalizadas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
      <input type="checkbox" @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo">
      <label :class="{ done:tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
    </li>
  </ul>
  </div>
</template>
<style scoped>

.done{
  text-decoration: line-through;
}
</style>

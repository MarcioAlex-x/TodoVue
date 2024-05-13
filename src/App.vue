<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaTarefas from './components/ListaTarefas.vue'

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
    <Cabecalho :tarefas-pendentes=getTarefasPendentes().length />
    <Formulario :trocar-filtro="e => estado.filtro = e.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="e => estado.tarefaTemp = e.target.value" :cadatrar-tarefa="cadastraTarefa" />
    <ListaTarefas :tarefas="getTarefasFiltradas()" />
    

  
  </div>
</template>
<style scoped>

</style>

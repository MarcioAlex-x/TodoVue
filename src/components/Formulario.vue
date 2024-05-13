
<script setup>
 const props = defineProps(['cadatrarTarefa', 'tarefaTemp','trocarFiltro','editaTarefaTemp'])
</script>
<template>
    <form @submit.prevent="props.cadatrarTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" requiredtype="text"
                    placeholder="Informe a nova tarefa!" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select class="form-control" @change="props.trocarFiltro">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Tarefas pendentes</option>
                    <option value="finalizadas">Tarefas finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>
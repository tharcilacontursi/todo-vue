<script setup>
const props = defineProps(['cadastraTarefa', 'tarefaTemporaria', 'trocarFiltro' , 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemporaria" @change="props.editaTarefaTemp" required type="text" placeholder="Digite aqui a descrição da tarefa " class="form-control">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Tarefas pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>
<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'


const estado = reactive({
  filtro: 'todas',
  tarefaTemporaria: '',
  tarefas: [
    {
    titulo: 'Estudar Es6',
    finalizada: false,
},
  {
  titulo: 'Estudar SASS',
    finalizada: false,
  },
  {
  titulo: 'Ir para a academia',
    finalizada: true,
  }
]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const filtro = estado.filtro;

  switch(filtro) {
    case 'pendentes':
      return getTarefasPendentes();
      case 'finalizadas':
      return  getTarefasFinalizadas();
      default:
        return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemporaria,
    finalizada: false, 
  }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemporaria = '';
    
}
</script>

<template>
<div class="container">
  <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"></Cabecalho>

  <Formulario> :trocarFiltro="evento => estado.filtro = evento.target.value" :tarefaTemporaria="estado.tarefaTemporaria" :editaTarefaTemp="evento => estado.tarefaTemporaria = evento.target.value" :cadastraTarefa="cadastraTarefa()" </Formulario>

  <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
</div>
</template>


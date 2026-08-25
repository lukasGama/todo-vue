<script setup>
    const props = defineProps(['tarefas']);
</script>

<template>
    <ul class="list-group mt-4">
        <li v-if="props.tarefas.length === 0" class="list-group-item text-center" >
            Não tem tarefas Pendentes
        </li>
        <li v-for="tarefa in props.tarefas" :key="tarefa.titulo" class="list-group-item"><!--usando a diretiva-->
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox"><!--Ultilizando o biden, começa com os dois pontos-->
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo"><!--ms= margin start-->
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>

.done {
    text-decoration: line-through;
    /*para add uma linha sobre o texto*/
}
</style>
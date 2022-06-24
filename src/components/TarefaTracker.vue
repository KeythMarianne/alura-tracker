<template>
    <BoxTracker>
        <div class="columns">
            <div class="column is-7">{{ tarefa.descricao || "Tarefa sem descrição" }}</div>
            <div class="column"><CronometroTracker :tempoEmSegundos="tarefa.duracaoEmSegundos"/></div>
        </div>
    </BoxTracker>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import CronometroTracker from './CronometroTracker.vue';
import ITarefa from '../interfaces/ITarefa'
import BoxTracker from './BoxTracker.vue';

export default defineComponent({
  name: 'TarefaTracker',
  components: {
    CronometroTracker,
    BoxTracker
  },
  props: {
    tarefa: {
        type: Object as PropType<ITarefa>,
        required: true
    }
  }
});
</script>

<style scoped>
.box {
    background: #FAF0CA;
}
</style>

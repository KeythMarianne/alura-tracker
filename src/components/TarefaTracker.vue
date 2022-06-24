<template>
    <div class="box has-text-weight-bold"> <!-- box tem texto mais forte -->
        <div class="columns">
            <div class="column is-7">{{ tarefa.descricao }}</div>
            <div class="column"><CronometroTracker :tempoEmSegundos="tarefa.duracaoEmSegundos"/></div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import CronometroTracker from './CronometroTracker.vue';
import ITarefa from '../interfaces/ITarefa'

export default defineComponent({
  name: 'TarefaTracker',
  components: {
    CronometroTracker
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

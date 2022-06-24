<template>
    <div class="box has-text-weight-bold"> <!-- box tem texto mais forte -->
        <slot>
            <!-- O que queremos dizer com esse slot é que o que estiver dentro do componente será renderizado no Box. -->
        </slot>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import CronometroTracker from './CronometroTracker.vue';
import ITarefa from '../interfaces/ITarefa'

export default defineComponent({
  name: 'BoxTracker',
});
</script>

<style scoped>
.box {
    background: #FAF0CA;
}
</style>

<template>
  <main class="columns is-gapless is-multiline"> <!--
    // main encapsula e faz o layout de colunas usando classe do Bulma
    // columns indica que dentro teremos várias colunas
    // is-gapless indica que o espaçamento entre essas colunas não existe
    // is-multiline indica que ele pode permitir múltiplas linhas. -->
    <div class="column is-one-fifths"> <!-- // tamanho = um quinto do tamanho disponível -->
      <BarraLateral />
    </div>

    <div class="column is-four-fifths"> <!-- // tamanho = quarto quintos do tamanho disponível -->
      <FormularioTracker />
    </div>
      
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue'
import FormularioTracker from './components/FormularioTracker.vue'

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    FormularioTracker
  }
});
</script>

<style>

</style>

// vs code, comentando no codigo varias linhas ao mesmo tempo
// ctrl + ;  comenta
// ctrl + ; descomenta
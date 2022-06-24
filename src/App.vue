<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro' : modoEscuroAtivo }"> <!--
    // main encapsula e faz o layout de colunas usando classe do Bulma
    // columns indica que dentro teremos várias colunas
    // is-gapless indica que o espaçamento entre essas colunas não existe
    // is-multiline indica que ele pode permitir múltiplas linhas. -->
    <div class="column is-one-fifths"> <!-- // tamanho = um quinto do tamanho disponível -->
      <BarraLateral @aoTemaAlterado="trocarTema" />
    </div>

    <div class="column is-four-fifths conteudo"> <!-- // tamanho = quarto quintos do tamanho disponível -->
      <FormularioTracker @aoSalvarTarefa="salvarTarefa" />
        <div class="lista-tarefas">
          <TarefaTracker v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>
          <BoxTracker v-if="listaEstaVazia">Você ainda não iniciou nenhuma tarefa.</BoxTracker>
        </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue'
import FormularioTracker from './components/FormularioTracker.vue'
import TarefaTracker from './components/TarefaTracker.vue'
import ITarefa from './interfaces/ITarefa'
import BoxTracker from './components/BoxTracker.vue'

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    FormularioTracker,
    TarefaTracker,
    BoxTracker
  },
  data () {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    }
  },
  computed: {
    listaEstaVazia() : boolean {
      return this.tarefas.length === 0 // pq 3 e não 2 sinais de igual?
    }
  },
  methods: {
    salvarTarefa (tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },
    trocarTema (modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo
    }
  }
});
</script>

<style>
.lista-tarefas {
  padding: 1.25rem;
}

main {
  --bg-primario: #fff;
  --texto-primario: #000;
}

main.modo-escuro {
  --bg-primario: #2b2d42; 
  --texto-primario: #ddd;
}

.conteudo {
  background-color: var(--bg-primario);
}

</style>

// vs code, comentando no codigo varias linhas ao mesmo tempo
// ctrl + ;  comenta
// ctrl + ; descomenta
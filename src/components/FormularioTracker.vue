<template>
    <div class="box">
        <div class="columns">
            <div class="column is-8" role="form" aria-label="Formulário para criação de uma nova tarefa">
                <input type="text" class="input" placeholder="Qual tarefa você deseja iniciar?" v-model="descricao"/> <!-- a propriedade v-model será responsável por linkar com o nosso estado a descrição da nossa tarefa: -->
            </div>
            <div class="column">
                <TemporizadorTracker @aoTemporizadorTrackerFinalizado="finalizarTarefa"/> <!-- no formulário vamos dizer que queremos ouvir um evento, então usamos o arroba -->
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import TemporizadorTracker from './TemporizadorTracker.vue';

export default defineComponent({
    name: 'FormularioTracker',
    emits: ['aoSalvarTarefa'],
    components: {
        TemporizadorTracker
    },
    data () { // Dado um input que meu usuário digitou, eu quero linkar com o meu estado. E agora preciso declarar esse estado. Então vou usar o data, que é o método que retorna o estado: data ( ) { return { descricao: ‘ ‘}. Então ele retorna um objeto que tem uma descrição que começa vazia.
        return {
            descricao: ''
        }
    },
    methods: {
        finalizarTarefa (tempoDecorrido: number) : void { // No nosso evento customizado estamos enviando o tempo em segundos. Então queremos receber number | E o “finalizarTarefa” é um método que não retorna nada, então fica :void
            //console.log('tempo da tarefa', tempoDecorrido)
            //console.log('descricao da tarefa', this.descricao)
            this.$emit('aoSalvarTarefa', {
                duracaoEmSegundos: tempoDecorrido,
                descricao: this.descricao
            })
            this.descricao = ''
        }
    }
});
</script>

<style scoped>
</style>
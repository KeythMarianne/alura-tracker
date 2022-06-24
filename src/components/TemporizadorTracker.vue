<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroTracker :tempoEmSegundos="tempoEmSegundos" /> <!-- passamos o nosso valor de tempo em segundos via prop para o componente cronômetro. Então ele espera um tempo em segundos também -->
        <BotaoTracker @clicado="iniciar" icone="fas fa-play" texto="play" :desabilitado="cronometroRodando" />
        <BotaoTracker @clicado="pausar" icone="fas fa-pause" texto="pause" :desabilitado="!cronometroRodando" />
        <BotaoTracker @clicado="finalizar" icone="fas fa-stop" texto="stop" :desabilitado="!cronometroRodando" />
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CronometroTracker from './CronometroTracker.vue';
import BotaoTracker from './BotaoTracker.vue';

export default defineComponent({
  components: {
    CronometroTracker,
    BotaoTracker
  },
  name: 'TemporizadorTracker',
  emits: ['aoTemporizadorTrackerFinalizado'],
  data () { //  o método data tem que retornar um objeto que representa quais são as informações pertinentes para esse componente
    return {
        tempoEmSegundos: 0,
        cronometro: 0,
        cronometroRodando: false
    }
  },
  methods: { // métodos são as funções que ele é capaz de executar dada a interação do usuário.
    iniciar () {
        // começar a contagem | 1 seg = 1000ms ou milissegundos
        // utilizando o JavaScript nós temos um método pronto para utilizar, chamado setInterval. Esse método vai receber dois parâmetros. O primeiro é o que de fato queremos fazer, então vamos passar uma arrow function vazia. E o segundo parâmetro é o intervalo de tempo que precisa ser calculado antes de ele ser executado novamente, em milissegundos. Temos que 1 segundo é igual a 1000 milissegundos. Então se queremos executar uma contagem a cada 1 segundo, vamos passar 1000. Ou seja, a cada 1 segundo ele vai ficar executando esse código.
        this.cronometroRodando = true
        this.cronometro = setInterval(() => {
            this.tempoEmSegundos += 1 // OU ++ | Eu tenho o this porque é este componente com essa propriedade. | passa um segundo e incrementa 1 e assim por diante.
        }, 1000)
        // console.log('iniciando');
    },
    pausar () {
        this.cronometroRodando = false
        clearInterval(this.cronometro)
        // console.log('pausando');        
    },
    finalizar () {
        this.cronometroRodando = false
        clearInterval(this.cronometro)
        this.$emit('aoTemporizadorTrackerFinalizado', this.tempoEmSegundos) // utilizar o $emit para criar eventos utilizados na comunicação entre componentes
        this.tempoEmSegundos = 0
        // console.log('finalizando');        
    }
  }
});
</script>

<style scoped>

</style>
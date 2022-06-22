<template>
    <div class="box">
        <div class="columns">
            <div class="column is-8" role="form" aria-label="Formulário para criação de uma nova tarefa">
                <input type="text" class="input" placeholder="Qual tarefa você deseja iniciar?" />
            </div>
            <div class="column">
                <div class="is-flex is-align-items-center is-justify-content-space-between">
                    <section>
                        <strong>
                            {{ tempoDecorrido }}
                        </strong>
                    </section>
                    <button class="button" @click="iniciar">
                        <span class="icon">
                            <i class="fas fa-play"></i>
                        </span>
                        <span>play</span>
                    </button>
                    <button class="button" @click="finalizar">
                        <span class="icon">
                            <i class="fas fa-stop"></i>
                        </span>
                        <span>stop</span>
                    </button> 
                </div>
            </div>
        </div>
    </div>
  
</template>

<script lang="ts">
import { defineComponent } from 'vue';


export default defineComponent({
  name: 'LadoFormulario',
  data () { //  o método data tem que retornar um objeto que representa quais são as informações pertinentes para esse componente
    return {
        tempoEmSegundos: 0,
        cronometro: 0
    }
  },
  computed: { // queremos uma informação dinâmica. Baseado no tempo em segundos essa informação vai ser computada. Então vamos usar o computed, que vai monitorar uma informação, e conforme essa informação for alterada ele vai reagir e vai se atualizar.
    tempoDecorrido () : string { // Para declararmos uma propriedade computada declaramos uma função. | string pq a função retorna string
        return new Date(this.tempoEmSegundos * 1000).toISOString().substr(11,8) // o newDate me da a data daquele momento. Eu não quero que seja o tempo atual. Eu quero que seja baseado no cálculo do “tempoEmSegundos”.E o construtor da data tem um método que recebe uma quantidade de milissegundos que representa uma data. Para conseguirmos atingir isso é só pegarmos o this.tempoEmSegundos * 1000. Lembrando que estamos utilizando o TypeScript. Esse método vai retornar uma string, vai pegar o tempo em segundos, multiplicar por 1000 para termos um tempo em milissegundos, e só estamos interessados na porção relacionada a hora, minuto e segundos. Nós podemos fazer um corte. Podemos chamar o método substr(), que vai recortar para nós. E a partir da posição 11 nós queremos 8: substr(11,8). Então já temos uma forma de pegar a data formatada bem simples.
    }
  },
  methods: { // métodos são as funções que ele é capaz de executar dada a interação do usuário.
    iniciar () {
        // começar a contagem | 1 seg = 1000ms ou milissegundos
        // utilizando o JavaScript nós temos um método pronto para utilizar, chamado setInterval. Esse método vai receber dois parâmetros. O primeiro é o que de fato queremos fazer, então vamos passar uma arrow function vazia. E o segundo parâmetro é o intervalo de tempo que precisa ser calculado antes de ele ser executado novamente, em milissegundos. Temos que 1 segundo é igual a 1000 milissegundos. Então se queremos executar uma contagem a cada 1 segundo, vamos passar 1000. Ou seja, a cada 1 segundo ele vai ficar executando esse código.
        this.cronometro = setInterval(() => {
            this.tempoEmSegundos += 1 // OU ++ | Eu tenho o this porque é este componente com essa propriedade. | passa um segundo e incrementa 1 e assim por diante.
        }, 1000)
        // console.log('iniciando');
    },
    finalizar () {
        clearInterval(this.cronometro)
        // console.log('finalizando');        
    }
  }
});
</script>

<style scoped>

</style>
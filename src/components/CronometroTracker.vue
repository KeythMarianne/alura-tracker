<template>
  <section>
    <strong>
      {{ tempoDecorrido }}
    </strong>
  </section>
</template>

<script lang="ts">

import { defineComponent } from 'vue';

export default defineComponent ({
    name: "CronometroTracker",
    props: { // Tudo que vamos receber do componente pai vai ficar dentro da nossa propriedade props.
        tempoEmSegundos: {
            type: Number, // O tipo dessa propriedade é um valor numérico, é um número inteiro que representa a quantidade de segundos decorrida, então type: Number
            default: 0 // podemos definir um valor padrão, então default: 0. Então por padrão esse tempo decorrido será 0.
        }
    },
    computed: { // queremos uma informação dinâmica. Baseado no tempo em segundos essa informação vai ser computada. Então vamos usar o computed, que vai monitorar uma informação, e conforme essa informação for alterada ele vai reagir e vai se atualizar.
        tempoDecorrido () : string { // Para declararmos uma propriedade computada declaramos uma função. | string pq a função retorna string
            return new Date(this.tempoEmSegundos * 1000).toISOString().substr(11,8) // o newDate me da a data daquele momento. Eu não quero que seja o tempo atual. Eu quero que seja baseado no cálculo do “tempoEmSegundos”.E o construtor da data tem um método que recebe uma quantidade de milissegundos que representa uma data. Para conseguirmos atingir isso é só pegarmos o this.tempoEmSegundos * 1000. Lembrando que estamos utilizando o TypeScript. Esse método vai retornar uma string, vai pegar o tempo em segundos, multiplicar por 1000 para termos um tempo em milissegundos, e só estamos interessados na porção relacionada a hora, minuto e segundos. Nós podemos fazer um corte. Podemos chamar o método substr(), que vai recortar para nós. E a partir da posição 11 nós queremos 8: substr(11,8). Então já temos uma forma de pegar a data formatada bem simples.
        }
    },
})

</script>

<style scoped>
</style>
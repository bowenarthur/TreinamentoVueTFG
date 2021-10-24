<template>
    <table class="Tabela" v-if="personagens && personagens.length > 0">
    <thead>
      <tr>
        <th>Personagem</th>
        <th>Ator/Atriz</th>
      </tr>
    </thead>
    <tbody v-for="personagem in personagens" :key="personagem._id">
      <tr v-on:click="removerPersonagem(personagem.nome)">
        <td>{{ personagem.nome }}</td>
        <td>{{ personagem.ator }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
    export default {
        props: {
            personagens: [Object]
        },
        methods: {
            removerPersonagem(nome) {
                this.$emit('remover-personagem', nome)
            }
        }
    }
</script>
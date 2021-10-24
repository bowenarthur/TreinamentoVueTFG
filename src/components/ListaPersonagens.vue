<template>
    <table class="Tabela" v-if="personagens.length > 0">
    <thead>
      <tr>
        <th>Personagem</th>
        <th>Ator/Atriz</th>
      </tr>
    </thead>
    <tbody v-for="personagem in personagens" :key="personagem._id">
      <tr>
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
        }
    }
</script>
<template>
  <h4>{{ Filme.nome }}</h4>
  <p>Sinopse: {{ Filme.sinopse }}</p>
  <p>Categoria: {{ Filme.categoria }}</p>
  <p>Duração: {{ Filme.duracao }}</p>
  <p>Ano: {{ Filme.ano }}</p>
  <p>Personagens:</p>
  <table class="Tabela">
    <thead>
      <tr>
        <th>Nome</th>
        <th>Ator/Atriz</th>
      </tr>
    </thead>
    <tbody v-for="personagem in Filme.personagens" :key="personagem._id">
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
    Filme: Object,
  },
};
</script>
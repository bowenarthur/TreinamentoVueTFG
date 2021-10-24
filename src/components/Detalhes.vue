<template>
  <h4>{{ filme.nome }}</h4>
  <p>Sinopse: {{ filme.sinopse }}</p>
  <p>Categoria: {{ filme.categoria }}</p>
  <p>Duração: {{ filme.duracao }}</p>
  <p>Ano: {{ filme.ano }}</p>
  <p>Personagens:</p>
  <table class="Tabela">
    <thead>
      <tr>
        <th>Nome</th>
        <th>Ator/Atriz</th>
      </tr>
    </thead>
    <tbody v-for="personagem in filme.personagens" :key="personagem._id">
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
    filme: Object,
  },
};
</script>
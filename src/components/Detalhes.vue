<template>
  <h4>{{ filme.nome }}</h4>
  <p>Sinopse: {{ filme.sinopse }}</p>
  <p>Categoria: {{ filme.categoria }}</p>
  <p>Duração: {{ filme.duracao }}</p>
  <p>Ano: {{ filme.ano }}</p>
  <ListaPersonagens :personagens="filme.personagens" />
</template>

<script>
    import ListaPersonagens from "./ListaPersonagens";

    export default {
        props: {
            filme: Object,
        },
        components: {
            ListaPersonagens
        }
    };
</script>
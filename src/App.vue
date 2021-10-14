<template>
  <div class="App">
    <Header />
    <ListaFilmes Titulo="Últimos filmes" />
    <ListaFilmes Titulo="Ação" Categoria="Ação" />
  </div>
</template>

<script>
import Header from "./components/Header";
import ListaFilmes from "./components/ListaFilmes";
export default {
  name: "App",
  data: () => ({
    filmes: [],
    filme: {},
    personagens: [],
    tipo: "",
    categoria: "",
    open: false,
    open1: false,
  }),
  components: {
    Header: Header,
    ListaFilmes: ListaFilmes,
  },
  methods: {},
};
</script>

<style>
</style>

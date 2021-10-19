<template>
  <div class="App">
    <Header />
    <ListaFilmes Titulo="Últimos filmes" />
    <ListaFilmes Titulo="Ação" Categoria="Ação" />
    <ListaFilmes Titulo="Fantasia" Categoria="Fantasia" />
  </div>
</template>

<script>
import Header from "./components/Header";
import ListaFilmes from "./components/ListaFilmes";
export default {
  name: "App",
  components: {
    Header: Header,
    ListaFilmes: ListaFilmes,
  },
};
</script>

<style>
</style>

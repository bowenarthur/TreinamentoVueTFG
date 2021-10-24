<template>
  <div class="App">
    <Header />
    <ListaFilmes Titulo="Últimos filmes" :filmes="filmes" v-on:mostrar-detalhes="mostrarDetalhes" />
    <div class="Modal" v-if="openDetalhes">
        <a class="close" v-on:click="fecharDetalhes"> &times; </a>
        <Detalhes :Filme="filme" />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import ListaFilmes from "./components/ListaFilmes";
import Detalhes from "./components/Detalhes"
import { lerFilmes } from "./Servico"

export default {
  name: "App",
  components: {
    Header,
    ListaFilmes,
    Detalhes
  },
  data() {
      return {
          filmes: [],
          filme: {},
          openDetalhes: false
      }
  },
  methods: {
      fetchData() {
          lerFilmes()
            .then(res => this.filmes = res.data)
      },
      mostrarDetalhes(filme) {
          this.filme = filme
          this.openDetalhes = true
      },
      fecharDetalhes() {
          this.filme = {}
          this.openDetalhes = false
      }
  },
  mounted() {
    const script = document.createElement("script");
    script.src =
      "https://cdnjs.cloudflare.com/ajax/libs/dragscroll/0.0.8/dragscroll.min.js";
    script.async = true;
    document.body.appendChild(script);
    this.fetchData()
  }
};
</script>
<template>
  <div class="app">
    <Header v-on:mostrar-form="mostrarForm" />
    <ListaFilmes 
        titulo="Últimos Filmes" 
        :filmes="filmes" 
        v-on:mostrar-detalhes="mostrarDetalhes"
        v-on:mostrar-form="mostrarForm" 
    />
    
    <ListaFilmes 
        titulo="Ação" 
        :filmes="acao" 
        v-on:mostrar-detalhes="mostrarDetalhes"
        v-on:mostrar-form="mostrarForm" 
    />

    <div class="modal" v-if="openDetalhes">
        <a class="close" v-on:click.prevent="fecharDetalhes"> &times; </a>
        <Detalhes :filme="filme" />
    </div>

    <div class="modal" v-if="openForm">
        <a class="close" v-on:click.prevent="fecharForm"> &times; </a>
        <Formulario :filme="filme" />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import ListaFilmes from "./components/ListaFilmes";
import Detalhes from "./components/Detalhes";
import Formulario from "./components/Formulario"
import { lerFilmes } from "./Servico"

export default {
  name: "App",
  components: {
    Header,
    ListaFilmes,
    Detalhes,
    Formulario
  },
  data() {
      return {
          filmes: [],
          filme: {},
          acao: [],
          openDetalhes: false,
          openForm: false
      }
  },
  methods: {
      fetchData() {
          lerFilmes().then(res => this.filmes = res.data)
          lerFilmes("Ação").then(res => this.acao = res.data)
      },
      mostrarDetalhes(filme) {
          this.filme = filme
          this.openDetalhes = true
          this.openForm = false
      },
      fecharDetalhes() {
          this.filme = {}
          this.openDetalhes = false
      },
      mostrarForm(filme) {
          this.filme = filme
          this.openForm = true
          this.openDetalhes = false
      },
      fecharForm() {
          this.filme = {}
          this.openForm = false
          this.fetchData()
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

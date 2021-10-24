<template>
  <div class="column">
    <div class="botoes">
      <a class="edit" v-on:click="this.mostrarCadastro()"> &#9998; </a>
      <a class="delete" v-on:click="this.deleteFilme(this.Filme._id)">
        &#128465;
      </a>
    </div>
    <div class="card" v-on:click="this.mostrarDetalhes()">
      <img alt="" :src="Filme.foto" />
      <p>{{ Filme.nome }}</p>
    </div>
  </div>

  <div class="Modal" v-if="open">
    <a class="close" v-on:click="this.closeModal()"> &times; </a>
    <Detalhes :Filme="Filme" />
  </div>

  <div class="Modal" v-if="open1">
    <a class="close" v-on:click="this.closeModal1()"> &times; </a>
    <Formulario :Filme="Filme" Tipo="Alterar" />
  </div>
</template>

<script>
import Formulario from "./Formulario";
import Detalhes from "./Detalhes";
import { excluirFilme } from '../Servico';
export default {
  data: () => ({
    open: false,
    open1: false,
  }),
  props: {
    Filme: Object,
  },
  components: {
    Formulario: Formulario,
    Detalhes: Detalhes,
  },
  methods: {
    mostrarCadastro() {
      this.open1 = true;
      this.open = false;
    },
    mostrarDetalhes() {
      this.open1 = false;
      this.open = true;
    },
    closeModal() {
      this.open = false;
      this.filme = {};
    },
    closeModal1() {
      this.open1 = false;
      this.filme = {};
    },
    deleteFilme(id) {
      excluirFilme(id);
    },
  },
};
</script>
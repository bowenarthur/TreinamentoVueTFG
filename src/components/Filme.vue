<template>
  <div class="column">
    <div class="botoes">
      <a class="edit" v-on:click="mostrarCadastro()"> &#9998; </a>
      <a class="delete" v-on:click="this.deleteFilme(this.Filme._id)">
        &#128465;
      </a>
    </div>
    <div class="card" v-on:click="mostrarDetalhes(Filme)">
      <img alt="" :src="Filme.foto" />
      <p>{{ Filme.nome }}</p>
    </div>
  </div>

  <div class="Modal" v-if="open1">
    <a class="close" v-on:click="this.closeModal1()"> &times; </a>
    <Formulario :Filme="Filme" Tipo="Alterar" />
  </div>
</template>

<script>
import Formulario from "./Formulario";
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
    Formulario
  },
  methods: {
    mostrarCadastro() {
      this.open1 = true;
      this.open = false;
    },
    mostrarDetalhes(filme) {
      this.$emit('mostrar-detalhes', filme)
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
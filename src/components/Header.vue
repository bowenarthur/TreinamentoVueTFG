<template>
  <div class="Header">
    <h3 class="TituloSite">LISTA DE FILMES</h3>
    <ul class="MenuSite">
      <li>
        <a v-on:click="this.mostrarCadastro()"> CADASTRAR FILME </a>
      </li>
    </ul>
  </div>
  <div class="Modal" v-if="open1">
    <a class="close" v-on:click="this.closeModal1()"> &times; </a>
    <Formulario Filme="" Tipo="Cadastro" />
  </div>
</template>

<script>
import Formulario from "./Formulario";
export default {
  data: () => ({
    open1: false,
  }),
  components: {
    Formulario: Formulario,
  },
  methods: {
    mostrarCadastro(filme, tipo) {
      this.open1 = true;
    },
    closeModal1() {
      this.open1 = false;
      this.filme = {};
    },
  },
};
</script>
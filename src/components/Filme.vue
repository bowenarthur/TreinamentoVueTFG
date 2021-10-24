<template>
  <div class="column">
    <div class="botoes">
      <a class="edit" v-on:click="mostrarForm(Filme)"> &#9998; </a>
      <a class="delete" v-on:click="this.deleteFilme(this.Filme._id)">
        &#128465;
      </a>
    </div>
    <div class="card" v-on:click="mostrarDetalhes(Filme)">
      <img alt="" :src="Filme.foto" />
      <p>{{ Filme.nome }}</p>
    </div>
  </div>
</template>

<script>
import { excluirFilme } from '../Servico';

export default {
  props: {
    Filme: Object,
  },
  methods: {
    mostrarForm(filme) {
      this.$emit('mostrar-form', filme);
    },
    mostrarDetalhes(filme) {
      this.$emit('mostrar-detalhes', filme);
    },
    deleteFilme(id) {
      excluirFilme(id);
    },
  },
};
</script>
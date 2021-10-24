<template>
  <div class="column">
    <div class="botoes">
      <a class="edit" v-on:click="mostrarForm"> &#9998; </a>
      <a class="delete" v-on:click="deleteFilme">
        &#128465;
      </a>
    </div>
    <div class="card" v-on:click="mostrarDetalhes">
      <img alt="" :src="filme.foto" />
      <p>{{ filme.nome }}</p>
    </div>
  </div>
</template>

<script>
import { excluirFilme } from '../Servico';

export default {
  props: {
    filme: Object,
  },
  methods: {
    mostrarForm() {
      this.$emit('mostrar-form', this.filme);
    },
    mostrarDetalhes() {
      this.$emit('mostrar-detalhes', this.filme);
    },
    deleteFilme() {
      excluirFilme(this.filme._id);
    },
  },
};
</script>
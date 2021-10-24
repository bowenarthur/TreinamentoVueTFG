<template>
  <div>
    <h3>{{ Titulo }}</h3>
    <div class="scrollmenu row dragscroll">
      <div v-for="filme in this.filmes" :key="filme._id">
        <Filme 
            :Filme="filme" 
            v-on:mostrar-detalhes="mostrarDetalhes" 
            v-on:mostrar-form="mostrarForm"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Filme from "./Filme";
export default {
  props: {
    Titulo: String,
    filmes: [Object]
  },
  components: {
    Filme
  },
  methods: {
      mostrarDetalhes(filme) {
          this.$emit('mostrar-detalhes', filme)
      },
      mostrarForm(filme) {
          this.$emit('mostrar-form', filme)
      }
  }
};
</script>
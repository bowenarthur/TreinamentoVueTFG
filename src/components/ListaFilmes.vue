<template>
  <div>
    <h3>{{ titulo }}</h3>
    <div class="scrollmenu row dragscroll">
      <div v-for="filme in filmes" :key="filme._id">
        <Filme 
            :filme="filme" 
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
    titulo: String,
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
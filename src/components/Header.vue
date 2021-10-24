<template>
  <div class="Header">
    <h3 class="TituloSite">LISTA DE FILMES</h3>
    <ul class="MenuSite">
      <li>
        <a v-on:click.prevent="mostrarForm"> CADASTRAR FILME </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  methods: {
    mostrarForm() {
      this.$emit('mostrar-form', {})
    }
  }
};
</script>
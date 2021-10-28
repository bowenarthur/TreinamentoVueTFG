<template>
  <div class="header">
    <h3 class="titulo-site">LISTA DE FILMES</h3>
    <ul class="menu-site">
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
<template>
  <div>
    <h3>{{ Titulo }}</h3>
    <div class="scrollmenu row dragscroll">
      <div v-for="filme in filmes" :key="filme._id">
        <Filme :Filme="filme" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Filme from "./Filme";
export default {
  data: () => ({
    filme: {},
    filmes: [],
  }),
  props: {
    Titulo: String,
    Categoria: String,
  },
  components: {
    Filme: Filme,
  },
  methods: {
    getFilmes() {
      axios
        .get(this.getURL())
        .then((res) => {
          this.filmes = res.data;
        })
        .catch((err) => console.log(err));
    },
    getURL() {
      return this.Categoria
        ? "https://frameworks-web.herokuapp.com/api/filmes?categoria=" +
            this.Categoria
        : "https://frameworks-web.herokuapp.com/api/filmes";
    },
  },
  mounted() {
    const script = document.createElement("script");
    script.src =
      "https://cdnjs.cloudflare.com/ajax/libs/dragscroll/0.0.8/dragscroll.min.js";
    script.async = true;
    document.body.appendChild(script);
    this.getFilmes();
  },
};
</script>
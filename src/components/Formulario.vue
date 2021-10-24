<template>
  <form v-on:submit.prevent="submit">
    <h2>Cadastro de Filme</h2>
    <div class="Formulario">
      <div>
        <label for="nome">Nome: </label>
        <input type="text" name="nome" v-model="nome" required />
        <br />
        <label for="foto">URL da foto: </label>
        <input type="text" name="foto" v-model="foto" required />
        <br />
        <label for="categoria">Categoria: </label>
        <select name="categoria" v-model="categoria" required>
          <option v-for="categoria in categorias" :value="categoria" v-bind:key="categoria">
            {{categoria}}
          </option>
        </select>
        <br />
        <label for="sinopse">Sinopse: </label>
        <textarea name="sinopse" v-model="sinopse" rows="3" required />
        <br />
        <label for="ano">Ano: </label>
        <input type="number" name="ano" v-model="ano" required />
        <br />
        <label for="duracao">Duração (min): </label>
        <input type="number" name="duracao" v-model="duracao" required />
        <br />
      </div>
      <EdicaoPersonagens 
        :personagens="personagens" 
        v-on:atualizar-personagens="atualizarPersonagens" 
      />
    </div>
    <input type="submit" class="BotaoCadastrar" value="Enviar" />
  </form>
</template>

<script>
import { inserirFilme, atualizarFilme } from "../Servico"
import EdicaoPersonagens from "./EdicaoPersonagens";

export default {
  data: () => ({
    personagens: [],
    nome: "",
    foto: "",
    categoria: "",
    sinopse: "",
    ano: "",
    duracao: "",
  }),
  props: {
    filme: Object
  },
  computed: {
    categorias: () => [
        "Ação", "Comédia", "Documentário", "Drama", "Fantasia", "Ficção", "Romance", "Terror"
    ]  
  },
  components: {
    EdicaoPersonagens
  },
  methods: {
    submit() {
      let data = {
        nome: this.nome,
        foto: this.foto,
        categoria: this.categoria,
        sinopse: this.sinopse,
        ano: this.ano,
        duracao: this.duracao,
        personagens: this.personagens,
      };
      this.filme._id ?
        atualizarFilme(this.filme._id, data) :
        inserirFilme(data);
    },
    atualizarPersonagens(personagens) {
        this.personagens = personagens
    }
  },
  mounted() {
    if (this.filme._id) {
      this.nome = this.filme.nome;
      this.foto = this.filme.foto;
      this.categoria = this.filme.categoria;
      this.sinopse = this.filme.sinopse;
      this.ano = this.filme.ano;
      this.duracao = this.filme.duracao;
      this.personagens = this.filme.personagens;
    } else {
      this.categoria = this.categorias[0]  
    }
  },
};
</script>
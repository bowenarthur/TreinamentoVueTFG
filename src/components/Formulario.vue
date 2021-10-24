<template>
  <form v-on:submit.prevent="this.submit()">
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
          <option disabled value=""></option>
          <option value="Ação">Ação</option>
          <option value="Comédia">Comédia</option>
          <option value="Documentário">Documentário</option>
          <option value="Drama">Drama</option>
          <option value="Fantasia">Fantasia</option>
          <option value="Ficção">Ficção</option>
          <option value="Romance">Romance</option>
          <option value="Terror">Terror</option>
        </select>
        <br />
        <label for="sinopse">Sinopse: </label>
        <textarea name="sinopse" v-model="sinopse" rows="3" required />
        <br />
        <label for="ano">Ano: </label>
        <input type="number" name="ano" v-model="ano" required />
        <br />
        <label for="duracao">Duração(minutos): </label>
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
import axios from "axios";
import EdicaoPersonagens from "./EdicaoPersonagens";

export default {
  data: () => ({
    personagens: [],
    nomepersonagem: "",
    ator: "",
    nome: "",
    foto: "",
    categoria: "",
    sinopse: "",
    ano: "",
    duracao: "",
  }),
  props: {
    Tipo: String,
    Filme: Object,
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
      if (this.Tipo === "Alterar") {
        axios
          .put(
            "https://frameworks-web.herokuapp.com/api/filmes/" + this.Filme._id,
            data
          )
          .then(() => {
            alert("Filme alterado com sucesso!");
            window.location.reload();
          })
          .catch((err) => {
            alert("Ocorreu um erro");
            console.log(err);
          });
      } else if (this.Tipo === "Cadastro") {
        axios
          .post("https://frameworks-web.herokuapp.com/api/filmes", data)
          .then(() => {
            alert("Filme cadastrado com sucesso!");
            window.location.reload();
          })
          .catch((err) => {
            alert("Ocorreu um erro");
            console.log(err);
          });
      } else console.log("Tipo incorreto");
    },
    atualizarPersonagens(personagens) {
        this.personagens = personagens
    }
  },
  mounted() {
    if (this.Filme) {
      this.nome = this.Filme.nome;
      this.foto = this.Filme.foto;
      this.categoria = this.Filme.categoria;
      this.sinopse = this.Filme.sinopse;
      this.ano = this.Filme.ano;
      this.duracao = this.Filme.duracao;
      this.personagens = this.Filme.personagens;
    }
  },
};
</script>
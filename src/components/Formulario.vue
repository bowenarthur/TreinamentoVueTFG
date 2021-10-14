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
        <label for="tempo">Duração: </label>
        <input type="text" name="tempo" v-model="tempo" required />
        <br />
      </div>
      <div>
        <h3>Personagens</h3>
        <br />
        <label for="nomepersonagem">Nome: </label>
        <input type="text" name="nomepersonagem" v-model="nomepersonagem" />
        <br />
        <label for="personagem">Ator/Atriz: </label>
        <input type="text" name="ator" v-model="ator" />
        <button type="button" v-on:click="this.adicionarPersonagem()">
          Adicionar
        </button>

        <table class="Tabela">
          <thead>
            <tr>
              <th>Nome</th>
              <th>Ator/Atriz</th>
            </tr>
          </thead>
          <tbody v-for="personagem in personagens" :key="personagem._id">
            <tr v-on:click="this.removerPersonagem(personagem.nome)">
              <td>{{ personagem.nome }}</td>
              <td>{{ personagem.ator }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <input type="submit" class="BotaoCadastrar" value="Enviar" />
  </form>
</template>

<script>
import axios from "axios";
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
    tempo: "",
  }),
  props: {
    Tipo: String,
    Filme: Object,
  },
  methods: {
    submit() {
      let data = {
        nome: this.nome,
        foto: this.foto,
        categoria: this.categoria,
        sinopse: this.sinopse,
        ano: this.ano,
        tempo: this.tempo,
        personagens: this.personagens,
      };
      if (this.Tipo === "Alterar") {
        axios
          .put(
            "https://frameworks-web.herokuapp.com/api/filmes/" + this.Filme._id,
            data
          )
          .then((res) => {
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
          .then((res) => {
            alert("Filme cadastrado com sucesso!");
            window.location.reload();
          })
          .catch((err) => {
            alert("Ocorreu um erro");
            console.log(err);
          });
      } else console.log("Tipo incorreto");
    },
    adicionarPersonagem() {
      let aux = this.personagens;
      if (aux) {
        aux[aux.length] = {
          nome: this.nomepersonagem,
          ator: this.ator,
        };
      } else {
        aux = [
          {
            nome: this.nomepersonagem,
            ator: this.ator,
          },
        ];
      }
      this.personagens = aux;
      this.nomepersonagem = "";
      this.ator = "";
    },
    removerPersonagem(nome) {
      let aux = this.personagens;
      let indice;
      aux.map(function (p, index) {
        if (p.nome === nome) {
          indice = index;
        }
      });
      aux.splice(indice, 1);
      this.personagens = aux;
      this.nomepersonagem = "";
      this.ator = "";
    },
  },
  mounted() {
    if (this.Filme) {
      this.nome = this.Filme.nome;
      this.foto = this.Filme.foto;
      this.categoria = this.Filme.categoria;
      this.sinopse = this.Filme.sinopse;
      this.ano = this.Filme.ano;
      this.tempo = this.Filme.tempo;
      this.personagens = this.Filme.personagens;
    }
  },
};
</script>
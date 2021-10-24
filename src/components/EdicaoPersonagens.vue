<template>
    <div>
        <h3>Personagens</h3>
        <br />
        <label for="nome">Nome: </label>
        <input type="text" name="nome" v-model="nome" />
        <br />
        <label for="ator">Ator/Atriz: </label>
        <input type="text" name="ator" v-model="ator" />
        <button type="button" v-on:click="adicionarPersonagem">
          Adicionar
        </button>
        <ListaPersonagens 
            :personagens="personagens" 
            v-on:remover-personagem="removerPersonagem" 
        />
    </div>
</template>

<script>
    import ListaPersonagens from "./ListaPersonagens";

    export default {
        data() {
            return {
                nome: "",
                ator: ""
            }
        },
        props: {
            personagens: [Object]
        },
        components: {
            ListaPersonagens
        },
        methods: {
            adicionarPersonagem() {
                if (this.nome.trim() != "" && this.ator.trim() != "") {
                    let personagens = this.personagens ?? []
                    personagens.push({nome: this.nome, ator: this.ator})

                    this.$emit('atualizar-personagens', personagens)

                    this.nome = ""
                    this.ator = ""
                }
            },
            removerPersonagem(nome) {
                const personagens = this.personagens
                    .filter(item => item.nome !== nome)
                this.$emit('atualizar-personagens', personagens)
            }
        }
    }
</script>
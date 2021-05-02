<template>
  <div id="filme">
    <div class="container" v-if="loading">
      <Loading />
    </div>
    <div class="container" v-else>
      <h2>{{ filme.nome }}</h2>
      <img v-bind:src="filme.foto" v-bind:alt="filme.nome" />
      <h3>Sinopse</h3>
      <p>{{ filme.sinopse }}</p>
      <div class="botoes">
        <router-link to="/" tag="button">Ver mais filmes</router-link>
        <button v-on:click="salvarFilme">Salvar</button>
        <a
          v-bind:href="`https://youtube.com/results?search_query=trailer+${filme.nome}+filme`"
          target="blank"
        >
          Trailer
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import api from "../services/api";
import Loading from "../components/Loading";
export default {
  name: "Filme",
  props: ["id"],
  components: {
    Loading,
  },
  data() {
    return {
      filme: {},
      loading: true,
    };
  },
  async created() {
    const response = await api.get(`?api=filmes/${this.id}`);
    this.filme = response.data;
    this.loading = false;
  },
  methods: {
    salvarFilme() {
      const minhaLista = localStorage.getItem("myFilme");

      let filmes = JSON.parse(minhaLista) || [];

      //Se tiver um filme com id igual ao que esta tentando adicionar devolve true
      const hasFilme = filmes.some((filme) => filme.id === this.filme.id);
      if (hasFilme) {
        alert("Você já tem esse filme salvo.");
        return;
        //Parar o codigo aqui
      }

      filmes.push(this.filme);
      localStorage.setItem("myFilme", JSON.stringify(filmes));
      alert("Filme salvo com sucesso!");
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  flex-direction: column;
  max-width: 900px;
}

h2 {
  color: #fff;
  margin-bottom: 0px;
  background: #c22323;
  padding: 15px;
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
}

.container img {
  width: 100%;
  border-bottom-left-radius: 20px;
  border-bottom-right-radius: 20px;
}

button {
  background-color: #ddd;
  margin-right: 5px;
  border-radius: 5px;
  margin-top: 15px;
  cursor: pointer;
  border: 0;
  padding: 12px;
  font-size: 20px;
  transition: all 0.5s;
  outline: none;
}
button:hover {
  background: #c22323;
  color: #fff;
}

a {
  background-color: #ddd;
  color: #000;
  margin-right: 5px;
  border-radius: 5px;
  margin-top: 15px;
  cursor: pointer;
  border: 0;
  padding: 12px;
  font-size: 20px;
  transition: all 0.5s;
  outline: none;
  text-decoration: none;
}

a:hover {
  color: #fff;
  background: #c22323;
}
</style>
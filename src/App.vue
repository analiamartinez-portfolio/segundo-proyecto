<template>
  <div id="app">
    <img alt="logo Pokemon" src="./assets/logoPokemon.jpeg" />
    <div>
      <b-table striped hover :items="listaPokemon.results" :fields="fields">
        <template #cell(name)="data">
          <h4 @click="getdetallesPokemon(data.item.url)">{{data.item.name.toUpperCase()}}</h4>
        </template>
      </b-table>
      <CardModal :detallesPokemon="detallesPokemon" />
    </div>
  </div>
</template>

<script>
import CardModal from "./components/CardModal.vue";
export default {
  name: "App",
  components: {
    CardModal
  },
  data() {
    return {
      listaPokemon: [],
      fields: ["name"],
      detallesPokemon: []
    };
  },

  methods: {
    async getListaPokemon() {
      try {
        const lista = await fetch("https://pokeapi.co/api/v2/pokemon");
        this.listaPokemon = await lista.json();
        console.log(this.listaPokemon);
      } catch (error) {
        console.log(error);
      }
    },
    async getdetallesPokemon(url) {
      try {
        const data = await fetch(url);
        this.detallesPokemon = await data.json();
        console.log(this.detallesPokemon);
      } catch (error) {
        console.log(error);
      } finally {
        this.$bvModal.show("cardPokemon");
      }
    }
  },
  created() {
    this.getListaPokemon();
  }
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h4 {
  font-weight: bold;
  color: rgb(225, 163, 69);
  cursor: pointer;
}
</style>

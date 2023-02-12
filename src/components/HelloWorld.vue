<template>
  <div class="hello">
    <h1>Wassurp</h1>
    <!-- <div v-for="nam in name" :key="nam">{{ nam.id + " \n" + nam.name }}</div> -->
    <label>{{ this.steamLink }}</label>
    <br>
    <button @click="fetchUsers"> Click mich </button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      steamID: "76561198064626725",
      appID: "730",
      apiKEY: "3145E11BDAF9CF494583334BE5FEF1BF",
      items:{},
    }
  },
  methods: {
    fetchUsers() {
      this.$http.get("https://steamcommunity.com/inventory/76561198064626725/730/2?l=english&count=5000")
        .then((result) => {
          this.items = result.data
        })
    }
  },
  computed: {
    steamLink() {
      return `http://api.steampowered.com/ISteamEconomy/GetPlayerItems/v0001/?key=${this.apiKEY}&steamid=${this.steamID}&appid=${this.appID}`
      // return `http://steamcommunity.com/inventory/${this.steamID}/${this.appID}/2?l=english&count=5000`
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>

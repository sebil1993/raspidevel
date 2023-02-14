<template>
  <div class="hello">
    <label>Vorhandene Items: {{ handleInventoryCount }}</label>
    <!-- <div v-for="asset in handleAssets" :key="asset">{{ asset[0] + " " + asset[1].classid + " " + getNameForClassID(asset[1].classid)  }}<br></div> -->
    <!-- <div class="w-screen bg-green-200">
      <table class="w-full flex justify-between">
        <tr class="">
          <th class="bg-gray-300 border-2 border-gray-400 w-full" v-for="identifier in tableNames" :key="identifier">
            {{ identifier }}</th>
        </tr>
      </table>
    </div> -->
    <div class="bg-green-200 px-20 flex justify-center">
      <table class="w-fit bg-gray-300 border-2 border-black">
        <thead >
          <tr class="flex justify-center">
            <th class="text-left px-10" v-for="identifier in tableNames" :key="identifier">
              {{ identifier }}</th>
          </tr>
        </thead>
        <tbody>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import json from "../assets/SteamInventory.json";
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      //https://steamcommunity.com/inventory/76561198064626725/730/2?l=english&count=5000
      items: json,
      tableNames: ["Number", "Class ID", "Market Name", "Quantity"]
    }
  },
  methods: {
    fetchUsers() {
      this.$http.get("http://steamcommunity.com/inventory/76561198064626725/730/2?l=english&count=5000")
        .then((result) => {
          this.items = result.data
        })
    },
    getNameForClassID(classID) {
      return this.handleDescriptions.find((e) => e[1].classid == classID)[1].market_name;
    }
  },
  computed: {
    steamLink() {
      return `http://api.steampowered.com/ISteamEconomy/GetPlayerItems/v0001/?key=${this.apiKEY}&steamid=${this.steamID}&appid=${this.appID}`
      // return `http://steamcommunity.com/inventory/${this.steamID}/${this.appID}/2?l=english&count=5000`
    },
    handleAssets() {
      // return Object.keys(this.items);
      return Object.entries(this.items.assets);
    },
    handleDescriptions() {
      // return Object.keys(this.items);
      return Object.entries(this.items.descriptions);
    },
    handleInventoryCount() {
      return Object.entries(this.items.assets).length;
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- <style scoped>
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
</style> -->

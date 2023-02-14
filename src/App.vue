<template>
  <div id="app">
    <ItemTable :items="finalItems"></ItemTable>
    {{ inventoryCount }}
    <!-- {{ countOccurencesForClassId(uniqueItems[1]) }}
    {{ uniqueItems }} -->
    <!-- <div v-for="item in uniqueItems" :key="item">
      {{ countOccurencesForClassId(item) + " " + getItemNameForClassId(item) }}
    </div> -->
    <!-- <div v-for="item in finalItems" :key="item">{{ item.name + " " + item.quantity }}</div> -->
  </div>
</template>

<script>
import ItemTable from './components/ItemTable.vue';
import json from "./assets/SteamInventory.json";

export default {
  name: 'App',
  components: {
    ItemTable
  },
  data() {
    return {
      finalItems: [],
    }
  },
  methods: {
    returnHello() {
      return "hello"
    },
    countOccurencesForClassId(classID) {
      let counter = 0;
      for (let i = 0; i < this.items.length; i++) {
        if (this.items[i] == classID) {
          counter++;
        }
      }
      return counter;
    },
    getItemNameForClassId(classID) {
      return this.descriptions.find((desc) => desc.class_id == classID).market_name;
    }
  },
  computed: {
    inventoryCount() {
      return Object.entries(json.assets).length;
    },
    descriptions() {
      return json.descriptions.map(desc => ({ market_name: desc.market_name, class_id: desc.classid }));
    },
    items() {
      return json.assets.map(item => item.classid)
    },
    uniqueItems() {
      return ([... new Set(this.items)]);
    },
  },
  created() {
    for (let i = 0; i < this.uniqueItems.length; i++) {
      let qqitem = {
        name: this.getItemNameForClassId(this.uniqueItems[i]),
        id: this.uniqueItems[i],
        quantity: this.countOccurencesForClassId(this.uniqueItems[i])
      }
      this.finalItems.push(qqitem);
    }
  }
}
</script>

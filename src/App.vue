<template>
  <div id="app">
    <div
      v-for="i in mapAsArray"
      :key="i.name">
      <div>{{ i.name }}</div>
      <div>{{ i.price }}</div>
    </div>
    <div @click="addItem('wangdao', 12)">add</div>
  </div>
</template>

<script>
/**
 * vue2 使用版本管理Map数据格式
 */
export default {
  name: "App",
  data() {
    return {
      list: new Map([
        ["Apple", { name: "Apple", price: 10 }],
        ["Banana", { name: "Banana", price: 5 }],
        ["Cherry", { name: "Cherry", price: 8 }],
      ]),
      mapVersion: 0, // 用来记录 Map 的版本
    };
  },
  computed: {
    mapAsArray() {
      this.mapVersion; // 建立依赖
      return Array.from(this.list.values());
    },
  },
  methods: {
    addItem(name, price) {
      this.mapVersion++;
      this.list.set(name, { name, price });
    },
    removeItem(name) {
      this.list.delete(name);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

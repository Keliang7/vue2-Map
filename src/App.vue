<template>
  <div id="app">
    <div
      v-for="i in mapAsArray"
      :key="i.name">
      <div>{{ i.name }}</div>
      <div>{{ i.price }}</div>
    </div>
    <div @click="addItem('wangdao', 12)">add</div>
    <div @click="addItem('Apple', 12)">set</div>
    <div @click="removeItem('Apple')">remove</div>

    <div>
      方法一、少量更新数据<br />
      使用 version 加 computed <br />
    </div>
    --------------------------------------------
    <div>
      方法二、大量更新数据 eg:socket实时数据更新<br />
      使用new Map(oldMap) <br />
      数据更新过程... <br />
      oldMap = newMap <br />
    </div>
    -------------------------------------------- <br />
    特别注意 使用方法一、更改数据的时候可以用get,也可以用set <br />
    使用方法二、更改数据的时候只能用set <br />
    get(i).property = value <br />
    set(i,{property:value}) 更改引用地址<br />
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
    setItem(name, price) {
      this.mapVersion++;
      this.list.get(name).price = price;
    },
    removeItem(name) {
      this.mapVersion++;
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

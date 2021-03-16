<template>
  <div class="todoListContainer">
    <div class="heading">
      <h2 id="title">Todo List</h2>
      <add-item-from v-on:reloadlist="getList()" />
    </div>
    <list-view :items="items" v-on:reloadlist="getList()" />
  </div>
</template>

<script>
import AddItemFrom from "./addItemFrom.vue";
import ListView from "./listView.vue";

export default {
  components: {
    AddItemFrom,
    ListView,
  },
  data: () => {
    return {
      items: [],
    };
  },
  methods: {
    getList() {
      axios
        .get("api/items")
        .then((res) => {
          this.items = res.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  created() {
    this.getList();
  },
};
</script>

<style scoped>
.todoListContainer {
  width: 350px;
  margin: auto;
}

.heading {
  background: #e6e6e6;
  padding: 10px;
}

#title {
  text-align: center;
}
</style>
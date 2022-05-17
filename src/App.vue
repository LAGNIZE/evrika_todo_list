<template>
  <div>
    <input v-model="value" id="search" />
    <button v-on:click="todo()">Добавить задачу</button>
  </div>
  <div v-for="todo in innerData.zadachi" v-bind:key="todo">
    <div
      v-if="innerData.activeFilter == 'active' && todo.active == true"
      style="display: flex; justify-content: center"
    >
      <div style="margin-right: 10px">
        {{ todo.text }}
      </div>
      <div v-on:click="remove(todo)">X</div>
    </div>
  </div>
  <div v-for="todo in innerData.zadachi" v-bind:key="todo">
    <div
      v-if="innerData.activeFilter == 'all'"
      style="display: flex; justify-content: center"
    >
      <div style="margin-right: 10px">
        {{ todo.text }}
      </div>
      <div v-on:click="remove(todo)">X</div>
    </div>
  </div>
  <div v-for="todo in innerData.zadachi" v-bind:key="todo">
    <div
      v-if="innerData.activeFilter == 'completed' && todo.active == false"
      style="display: flex; justify-content: center"
    >
      <div style="margin-right: 10px">
        {{ todo.text }}
      </div>
      <div v-on:click="remove(todo)">X</div>
    </div>
  </div>
  <div>
    <span style="margin-right: 10px" v-on:click="setFilter('active')"
      >Активные</span
    >
    <span style="margin-right: 10px" v-on:click="setFilter('all')">Все</span>
    <span style="margin-right: 10px" v-on:click="setFilter('completed')"
      >Завершенные</span
    >
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      innerData: {
        zadachi: [],
        activeFilter: "all",
      },
      value: "Задача 1",
    };
  },
  created() {
    function fetchData() {
      return fetch(
        "https://my-json-server.typicode.com/falk20/demo/todos"
      ).then((response) => response.json());
    }
    fetchData().then((value) => (this.innerData.zadachi = value));
  },
  methods: {
    todo() {
      this.todo.id = Date.now();
      this.todo.active = true;
      this.innerData.zadachi.push({
        text: this.value,
        id: this.todo.id,
        active: this.todo.active,
      });
    },
    setFilter(filter) {
      this.innerData.activeFilter = filter;
    },
    remove(post) {
      this.innerData.zadachi = this.innerData.zadachi.filter(
        (p) => p.id !== post.id
      );
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

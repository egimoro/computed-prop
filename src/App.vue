<script>
import WatchPropVue from "./components/WatchProp.vue";
import TodoPropVue from "./components/TodoProp.vue";

const routes = {
  "/": TodoPropVue,
  "/watch": WatchPropVue,
};

export default {
  data() {
    return {
      currentPath: window.location.hash,
    };
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || "/"];
    },
  },
  mounted() {
    window.addEventListener("hashchange", () => {
      this.currentPath = window.location.hash;
    });
  },
};
</script>

<template>
  <ul class="nav">
    <li><a class="active" href="#/">Todo</a></li>
    <li><a href="#/watch">WatchProp</a></li>
  </ul>
  <component :is="currentView" />
</template>
<style>
ul.nav {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #0677a1;
}

.nav li {
  float: left;
}

li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

li a:hover:not(.active) {
  background-color: rgba(37, 180, 37, 0.918);
}

.active {
  background-color: #04aa6d;
}
</style>

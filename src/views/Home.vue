<template>
  <div class="home container-lg">
    <h1>Gihub Framework Watcher</h1>
    <div>
      <table class="table">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Framework</th>
            <th scope="col">Stars</th>
            <th scope="col">Watchers</th>
            <th scope="col">Forks</th>
            <th scope="col">Popularity</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <th scope="row">1</th>
            <td>Vue</td>
            <td>{{ this.vue["watchers"] }}</td>
            <td>{{ this.vue["subscribers_count"] }}</td>
            <td>{{ this.vue["forks"] }}</td>
            <td>{{ parseInt((this.vue["watchers"] + this.vue["forks"] + this.vue["subscribers_count"]) / 3) }}</td>
          </tr>
          <tr>
            <th scope="row">2</th>
            <td>Angular</td>
            <td>{{ this.angular["watchers"] }}</td>
            <td>{{ this.angular["subscribers_count"] }}</td>
            <td>{{ this.angular["forks"] }}</td>
            <td>
              {{ parseInt((this.angular["watchers"] + this.angular["forks"] + this.angular["subscribers_count"]) / 3) }}
            </td>
          </tr>
          <tr>
            <th scope="row">3</th>
            <td>Ember</td>
            <td>{{ this.ember["watchers"] }}</td>
            <td>{{ this.ember["subscribers_count"] }}</td>
            <td>{{ this.ember["forks"] }}</td>
            <td>
              {{ parseInt((this.ember["watchers"] + this.ember["forks"] + this.ember["subscribers_count"]) / 3) }}
            </td>
          </tr>
          <tr>
            <th scope="row">4</th>
            <td>Svelte</td>
            <td>{{ this.svelte["watchers"] }}</td>
            <td>{{ this.svelte["subscribers_count"] }}</td>
            <td>{{ this.svelte["forks"] }}</td>
            <td>
              {{ parseInt((this.svelte["watchers"] + this.svelte["forks"] + this.svelte["subscribers_count"]) / 3) }}
            </td>
          </tr>
          <tr>
            <th scope="row">5</th>
            <td>React</td>
            <td>{{ this.react["watchers"] }}</td>
            <td>{{ this.react["subscribers_count"] }}</td>
            <td>{{ this.react["forks"] }}</td>
            <td>
              {{ parseInt((this.react["watchers"] + this.react["forks"] + this.react["subscribers_count"]) / 3) }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      vue: {},
      angular: {},
      ember: {},
      svelte: {},
      react: {},
    };
  },
  created: function () {
    this.getWatcherData();
  },
  mounted: function () {},
  methods: {
    getWatcherData: function () {
      axios.get("https://api.github.com/repos/vuejs/vue").then((response) => {
        console.log(response.data);
        this.vue = response.data;
        console.log();
      });
      axios.get("https://api.github.com/repos/angular/angular.js").then((response) => {
        console.log(response.data);
        this.angular = response.data;
        console.log();
      });
      axios.get("https://api.github.com/repos/emberjs/ember.js").then((response) => {
        console.log(response.data);
        this.ember = response.data;
        console.log();
      });
      axios.get("https://api.github.com/repos/sveltejs/svelte").then((response) => {
        console.log(response.data);
        this.svelte = response.data;
        console.log();
      });
      axios.get("https://api.github.com/repos/facebook/react").then((response) => {
        console.log(response.data);
        this.react = response.data;
        console.log();
      });
    },
  },
};
</script>

<template>
  <div class="home container-lg mt-5">
    <h1>Github Framework Watcher</h1>
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
            <td>{{ this.vue["pop"] }}</td>
          </tr>
          <tr>
            <th scope="row">2</th>
            <td>Angular</td>
            <td>{{ this.angular["watchers"] }}</td>
            <td>{{ this.angular["subscribers_count"] }}</td>
            <td>{{ this.angular["forks"] }}</td>
            <td>{{ this.angular["pop"] }}</td>
          </tr>
          <tr>
            <th scope="row">3</th>
            <td>Ember</td>
            <td>{{ this.ember["watchers"] }}</td>
            <td>{{ this.ember["subscribers_count"] }}</td>
            <td>{{ this.ember["forks"] }}</td>
            <td>{{ this.ember["pop"] }}</td>
          </tr>
          <tr>
            <th scope="row">4</th>
            <td>Svelte</td>
            <td>{{ this.svelte["watchers"] }}</td>
            <td>{{ this.svelte["subscribers_count"] }}</td>
            <td>{{ this.svelte["forks"] }}</td>
            <td>{{ this.svelte["pop"] }}</td>
          </tr>
          <tr>
            <th scope="row">5</th>
            <td>React</td>
            <td>{{ this.react["watchers"] }}</td>
            <td>{{ this.react["subscribers_count"] }}</td>
            <td>{{ this.react["forks"] }}</td>
            <td>{{ this.react["pop"] }}</td>
          </tr>
        </tbody>
      </table>

      <div v-if="loaded" class="container">
        <bar-chart v-if="loaded" :chartData="chartData" :options="options" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import BarChart from "../views/Chart.vue";

export default {
  name: "BarChartContainer",
  components: { BarChart },
  data: function () {
    return {
      chartData: {},
      options: {
        scales: {
          yAxes: [
            {
              ticks: {
                beginAtZero: true,
              },
              gridLines: {
                display: true,
              },
            },
          ],
          xAxes: [
            {
              gridLines: {
                display: false,
              },
            },
          ],
        },
        legend: {
          display: true,
        },
        responsive: true,
        maintainAspectRatio: false,
      },
      loaded: false,
      test: "hello",
      vue: {},
      angular: {},
      ember: {},
      svelte: {},
      react: {},
    };
  },
  created: function () {},
  mounted: async function () {
    this.getWatcherData();
  },
  methods: {
    getWatcherData: function () {
      axios.get("https://api.github.com/repos/vuejs/vue").then((response) => {
        this.vue = response.data;
        this.vue["pop"] = parseInt((this.vue["watchers"] + this.vue["forks"] + this.vue["subscribers_count"]) / 3);
        this.setChartData();
      });
      axios.get("https://api.github.com/repos/angular/angular.js").then((response) => {
        this.angular = response.data;
        this.angular["pop"] = parseInt(
          (this.angular["watchers"] + this.angular["forks"] + this.angular["subscribers_count"]) / 3
        );
      });
      axios.get("https://api.github.com/repos/emberjs/ember.js").then((response) => {
        this.ember = response.data;
        this.ember["pop"] = parseInt(
          (this.ember["watchers"] + this.ember["forks"] + this.ember["subscribers_count"]) / 3
        );
      });
      axios.get("https://api.github.com/repos/sveltejs/svelte").then((response) => {
        this.svelte = response.data;
        this.svelte["pop"] = parseInt(
          (this.svelte["watchers"] + this.svelte["forks"] + this.svelte["subscribers_count"]) / 3
        );
      });
      axios
        .get("https://api.github.com/repos/facebook/react")
        .then((response) => {
          this.react = response.data;
          this.react["pop"] = parseInt(
            (this.react["watchers"] + this.react["forks"] + this.react["subscribers_count"]) / 3
          );
          this.setChartData();
        })
        .then();
      console.log("calls done");
      this.test = "goodbye";
    },
    setChartData: function () {
      this.chartData = {
        datasets: [
          {
            label: "Vue",
            borderWidth: 1,
            backgroundColor: [
              "rgba(255, 99, 132, 0.2)",
              "rgba(255, 99, 132, 0.2)",
              "rgba(255, 99, 132, 0.2)",
              "rgba(255, 99, 132, 0.2)",
            ],
            borderColor: ["rgba(255,99,132,1)", "rgba(255,99,132,1)", "rgba(255,99,132,1)", "rgba(255,99,132,1)"],
            pointBorderColor: "#2554FF",
            data: [this.vue["watchers"], this.vue["forks"], this.vue["subscribers_count"], this.vue["pop"]],
          },
          {
            label: "Angular",
            borderWidth: 1,
            backgroundColor: [
              "rgba(54, 162, 235, 0.2)",
              "rgba(54, 162, 235, 0.2)",
              "rgba(54, 162, 235, 0.2)",
              "rgba(54, 162, 235, 0.2)",
            ],
            borderColor: [
              "rgba(54, 162, 235, 1)",
              "rgba(54, 162, 235, 1)",
              "rgba(54, 162, 235, 1)",
              "rgba(54, 162, 235, 1)",
            ],
            pointBorderColor: "blue",
            data: [
              this.angular["watchers"],
              this.angular["forks"],
              this.angular["subscribers_count"],
              this.angular["pop"],
            ],
          },
          {
            label: "Ember",
            borderWidth: 1,
            backgroundColor: [
              "rgba(255, 206, 86, 0.2)",
              "rgba(255, 206, 86, 0.2)",
              "rgba(255, 206, 86, 0.2)",
              "rgba(255, 206, 86, 0.2)",
            ],
            borderColor: [
              "rgba(255, 206, 86, 1)",
              "rgba(255, 206, 86, 1)",
              "rgba(255, 206, 86, 1)",
              "rgba(255, 206, 86, 1)",
            ],
            pointBorderColor: "#2554FF",
            data: [this.ember["watchers"], this.ember["forks"], this.ember["subscribers_count"], this.ember["pop"]],
          },
          {
            label: "Svelte",
            borderWidth: 1,
            backgroundColor: [
              "rgba(75, 192, 192, 0.2)",
              "rgba(75, 192, 192, 0.2)",
              "rgba(75, 192, 192, 0.2)",
              "rgba(75, 192, 192, 0.2)",
            ],
            borderColor: [
              "rgba(75, 192, 192, 1)",
              "rgba(75, 192, 192, 1)",
              "rgba(75, 192, 192, 1)",
              "rgba(75, 192, 192, 1)",
            ],
            pointBorderColor: "#2554FF",
            data: [this.svelte["watchers"], this.svelte["forks"], this.svelte["subscribers_count"], this.svelte["pop"]],
          },
          {
            label: "React",
            borderWidth: 1,
            backgroundColor: [
              "rgba(153, 102, 255, 0.2)",
              "rgba(153, 102, 255, 0.2)",
              "rgba(153, 102, 255, 0.2)",
              "rgba(153, 102, 255, 0.2)",
            ],
            borderColor: [
              "rgba(153, 102, 255, 1)",
              "rgba(153, 102, 255, 1)",
              "rgba(153, 102, 255, 1)",
              "rgba(153, 102, 255, 1)",
            ],
            pointBorderColor: "#2554FF",
            data: [this.react["watchers"], this.react["forks"], this.react["subscribers_count"], this.react["pop"]],
          },
        ],
        labels: ["Stars", "Watchers", "Forks", "Popularity"],
      };
      this.loaded = true;
      console.log(this.vue);
      console.log(this.react["watchers"]);
    },
  },
};
</script>

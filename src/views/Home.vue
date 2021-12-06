<template>
  <div class="home container-lg">
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

      <div class="container">
        <h3>Graph</h3>
        <Chart :chartdata="chartData" :options="options"></Chart>
      </div>
      <canvas></canvas>
    </div>
  </div>
</template>

<script>
import axios from "axios";
// import VueCharts from "vue-chartjs";
import Chart from "../views/Chart.vue";
export default {
  components: { Chart },
  data: function () {
    return {
      chartData: {
        labels: [
          "2015-01",
          "2015-02",
          "2015-03",
          "2015-04",
          "2015-05",
          "2015-06",
          "2015-07",
          "2015-08",
          "2015-09",
          "2015-10",
          "2015-11",
          "2015-12",
        ],
        datasets: [
          {
            label: "Bar Chart",
            borderWidth: 1,
            backgroundColor: [
              "rgba(255, 99, 132, 0.2)",
              "rgba(54, 162, 235, 0.2)",
              "rgba(255, 206, 86, 0.2)",
              "rgba(75, 192, 192, 0.2)",
              "rgba(153, 102, 255, 0.2)",
              "rgba(255, 159, 64, 0.2)",
              "rgba(255, 99, 132, 0.2)",
              "rgba(54, 162, 235, 0.2)",
              "rgba(255, 206, 86, 0.2)",
              "rgba(75, 192, 192, 0.2)",
              "rgba(153, 102, 255, 0.2)",
              "rgba(255, 159, 64, 0.2)",
            ],
            borderColor: [
              "rgba(255,99,132,1)",
              "rgba(54, 162, 235, 1)",
              "rgba(255, 206, 86, 1)",
              "rgba(75, 192, 192, 1)",
              "rgba(153, 102, 255, 1)",
              "rgba(255, 159, 64, 1)",
              "rgba(255,99,132,1)",
              "rgba(54, 162, 235, 1)",
              "rgba(255, 206, 86, 1)",
              "rgba(75, 192, 192, 1)",
              "rgba(153, 102, 255, 1)",
              "rgba(255, 159, 64, 1)",
            ],
            pointBorderColor: "#2554FF",
            data: [12, 19, 3, 5, 2, 3, 20, 3, 5, 6, 2, 1],
          },
        ],
      },
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
  mounted: function () {
    this.renderChart({
      labels: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ],
      datasets: [
        {
          label: "GitHub Commits",
          backgroundColor: "#f87979",
          data: [40, 20, 12, 39, 10, 40, 39, 80, 40, 20, 12, 11],
        },
      ],
    }),
      this.setChartData();
  },
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
      this.loaded = true;
    },
    setChartData: function () {
      this.props["chartData"]["data"]["data"].push(1);
    },
  },
};
</script>

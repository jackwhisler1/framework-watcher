<script>
// import VueCharts from "vue-chartjs";
import { Bar } from "vue-chartjs";

export default {
  extends: Bar,
  mounted: function () {
    this.renderChart({});
  },
};
</script>

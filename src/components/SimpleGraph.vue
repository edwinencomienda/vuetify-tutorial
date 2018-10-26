
<script>
import { Bar, mixins } from 'vue-chartjs'

export default {
  extends: Bar,
  mixins: [mixins.reactiveProp],
  props: ['chartData'],
  mounted () {
    const options = {} // this is the options for something you want for the graph please see the documentation.
    // Overwriting base render method with actual data.
    this.renderChart(this.chartData, options)
  }
}
</script>

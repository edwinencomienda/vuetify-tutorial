<template>
  <div>
    <v-layout mb-4>
      <v-flex xs4>
          <simple-graph :chartData="chartData"></simple-graph>
      </v-flex>
    </v-layout>
    <v-layout>
      <v-flex xs12>
          <v-data-table :loading="loading" :headers="headers" :items="items" hide-actions class="elevation-1">
              <template slot="items" slot-scope="props">
                <td class="py-2">
                  <v-avatar>
                    <img
                      src="https://avatars1.githubusercontent.com/u/26597108?s=460&v=4"
                      alt="John"
                    >
                  </v-avatar>
                </td>
                <td>{{ props.item.id }}</td>
                <td>
                    <router-link :to="`/details/${props.item.id}`">{{ props.item.title }}</router-link>
                </td>
                <td>{{ props.item.completed }}</td>
                <td>
                    <v-progress-linear :value="Math.floor(Math.random() * 100)"></v-progress-linear>
                </td>
                <td class="text-xs-center">
                    <v-btn small fab dark color="indigo">
                        <v-icon dark>edit</v-icon>
                    </v-btn>
                </td>
              </template>
          </v-data-table>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import SimpleGraph from '../components/SimpleGraph'

export default {
  components: {
    SimpleGraph
  },
  data () {
    return {
      items: [],
      headers: [
        { text: '', value: '', sortable: false, width: '1%' },
        { text: 'Id', value: 'id' },
        { text: 'Title', value: 'title' },
        { text: 'completed', value: 'completed' },
        { text: 'Usage', value: '' },
        { text: 'Actions', value: '', sortable: false, width: '1%', class: 'text-xs-center' },
      ],
      loading: false,
      chartData: ''
    }
  },
  created () {
    this.getData()
    this.getGraphData()
  },
  methods: {
    getData () {
      this.loading = true
      axios.get('https://jsonplaceholder.typicode.com/todos').then(response => {
        this.items = response.data
        this.loading = false
      })
    },
    getGraphData () {
      axios.get('https://api.myjson.com/bins/159c64').then(response => {
        this.chartData = {
          labels: response.data.labels,
          datasets: [
            {
              label: 'GitHub Commits',
              backgroundColor: '#3f51b5',
              data: response.data.data
            }
          ]
        }
      })
    }
  }
}
</script>

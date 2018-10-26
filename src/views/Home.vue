<template>
  <div>
    <v-layout mb-4>
      <v-flex xs4>
          <simple-graph></simple-graph>
      </v-flex>
    </v-layout>
    <v-layout>
      <v-flex xs12>
          <v-data-table :loading="loading" :headers="headers" :items="items" hide-actions class="elevation-1">
              <template slot="items" slot-scope="props">
                <td class="py-2">
                  <v-avatar>
                    <img
                      src="https://cdn.vuetifyjs.com/images/john.jpg"
                      alt="John"
                    >
                  </v-avatar>
                </td>
                <td><router-link to="/details">{{ props.item.type }}</router-link></td>
                <td>{{ props.item.name }}</td>
                <td>{{ props.item.status }}</td>
                <td>
                    <v-progress-linear :value="Math.floor(Math.random() * 100)"></v-progress-linear>
                </td>
                <td class="text-xs-center">
                    <v-btn small fab dark color="indigo">
                        <v-icon dark>add</v-icon>
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
        { text: 'Type', value: 'type' },
        { text: 'Name', value: 'name' },
        { text: 'Status', value: 'status' },
        { text: 'Usage', value: '' },
        { text: 'Actions', value: '', sortable: false, width: '1%', class: 'text-xs-center' },
      ],
      loading: false
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.loading = true
      axios.get('https://api.myjson.com/bins/8wtbw').then(response => {
        this.items = response.data.items
        this.loading = false
      })
    }
  }
}
</script>

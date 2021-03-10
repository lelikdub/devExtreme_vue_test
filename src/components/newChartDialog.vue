<template>
  <v-dialog
      v-model="show"
      @click:outside="closeModal"
      max-width="890"
  >
    <v-card>
      <v-card-title>
        <h3>
          Создать график
        </h3>
        <v-spacer />
        <v-btn
            icon
            @click="closeModal"
        >
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </v-card-title>
      <v-card-text>
        <v-row class="mx-6 my-2">
          <v-col>
            <v-select
                v-model="chartTypeSelected"
                :items="chartType"
                item-text="name"
                item-value="id"
                label="Выберите тип графика"
                @change="dataSourceSelected = null"
                outlined
            ></v-select>
            <v-select
                v-model="dataSourceSelected"
                :items="suitableDataSources"
                item-text="name"
                item-value="id"
                label="Выберите источник данных"
                outlined
            ></v-select>
          </v-col>
        </v-row>
      </v-card-text>
      <v-card-actions>
        <v-btn
            block
            color="primary"
            :disabled="!canAddChart"
            :loading="dataLoading"
            @click="addChart"
        >
          Создать
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
const axios = require('axios');

export default {
  name: "newChartDialog",
  props: {
    show: Boolean,
  },
  computed: {
    canAddChart () {
      return this.chartTypeSelected && this.dataSourceSelected
    },
    suitableDataSources () {
      return this.dataSource.filter(source => source.chartType === this.chartTypeSelected) || []
    }
  },
  data () {
    return {
      dataLoading: false,
      chartTypeSelected: null,
      chartType: [
        {
          id: 1,
          name: 'Pie chart',
        },
        {
          id: 2,
          name: 'Line chart',
        },
      ],
      dataSourceSelected: null,
      dataSource: [
        {
          chartType: 1,
          id: 1,
          name: 'Data for Pie chart',
          link: 'https://run.mocky.io/v3/2699115b-8ced-40c3-8072-b7fa9faf6047',
        },
        {
          chartType: 2,
          id: 2,
          name: 'Data for Line chart',
          link: 'https://run.mocky.io/v3/92a0a266-0321-4ff5-9993-b394d03ceee2',
        },
        {
          chartType: 2,
          id: 3,
          name: 'Other data for Line chart',
          link: 'https://run.mocky.io/v3/92a0a266-0321-4ff5-9993-b394d03ceee2',
        }
      ]
    }
  },
  methods: {
    addChart () {
      this.dataLoading = true
      const url = this.dataSource.find(value => value.id === this.dataSourceSelected).link
      axios.get(url).then((resp) => {
        this.dataLoading = false
        this.$emit('newChart', { chartType: this.chartTypeSelected, chartData: resp.data })
      }).catch((e) => {
        console.log('Error:', e)
        this.dataLoading = false
      })
    },
    closeModal () {
      this.$emit('close')
    }
  },

}
</script>

<style scoped>

</style>

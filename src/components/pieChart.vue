<template>
  <v-row class="text-center mx-6 my-6">
    <v-col cols="12">
      <DxPieChart
          id="pie"
          :data-source="chartData"
          palette="Green"
      >
        <DxSeries
            argument-field="Группа"
            value-field="Доля"
        >
          <DxLabel
              :visible="true"
              :customize-text="formatLabel"
              position="columns"
          >
            <DxConnector
                :visible="true"
                :width="0.5"
            />
            <DxFont :size="16"/>
          </DxLabel>
        </DxSeries>
        <DxLegend
            :column-count="4"
            orientation="horizontal"
            item-text-position="right"
            horizontal-alignment="center"
            vertical-alignment="bottom"
        />
        <DxExport :enabled="true"/>
      </DxPieChart>
    </v-col>
  </v-row>
</template>

<script>
import DxPieChart, {
  DxSeries,
  DxLegend,
  DxLabel,
  DxConnector,
  DxFont,
  DxExport
} from 'devextreme-vue/pie-chart'

export default {
  name: "chart",
  props: {
    chartData: Array
  },
  components: {
    DxPieChart,
    DxSeries,
    DxLegend,
    DxLabel,
    DxConnector,
    DxFont,
    DxExport
  },
  methods: {
    formatLabel(pointInfo) {
      return `${pointInfo.valueText} %`
    }
  },
}
</script>

<style scoped>

</style>

<template>
  <v-row class="text-center mx-10 my-8">
    <v-col cols="12">
      <DxChart
          :data-source="chartData"
          palette="material"
      >
        <DxSize :height="420"/>
        <DxValueAxis>
          <DxLabel
              :visible="true"
          />
        </DxValueAxis>
        <DxSeries
            argument-field="Дата"
            value-field="Процент"
            :type="type"
            name="Процент"
            color="#41C83D"
        />
        <DxLegend :visible="true"/>
        <DxExport :enabled="true"/>
        <DxLoadingIndicator :enabled="true"/>
      </DxChart>
    </v-col>
  </v-row>
</template>

<script>
import DxChart, {
  DxValueAxis,
  DxLabel,
  DxLegend,
  DxExport,
  DxSeries,
  DxSize,
  DxLoadingIndicator
} from 'devextreme-vue/chart';

export default {
  name: "chart",
  props: {
    chartData: Array
  },
  components: {
    DxChart,
    DxValueAxis,
    DxLabel,
    DxLegend,
    DxExport,
    DxLoadingIndicator,
    DxSeries,
    DxSize,
  },
  data () {
    return {
      type: 'line'
    }
  },
}
</script>

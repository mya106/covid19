<template>
  <data-view :title="title">
    <template v-slot:button>
      <data-selector v-model="dataKind" />
    </template>
    <bar :chart-data="displayData" :options="chartOption" :height="240" />
  </data-view>
</template>

<style></style>

<script>
import DataView from '@/components/DataView.vue'
import DataSelector from '@/components/DataSelector.vue'

export default {
  components: { DataView, DataSelector },
  props: {
    title: {
      type: String,
      required: false,
      default: ''
    },
    chartData: {
      type: Array,
      required: false,
      default: () => []
    },
    chartOption: {
      type: Object,
      required: false,
      default: () => {}
    }
  },
  data() {
    return {
      dataKind: 'transition'
    }
  },
  computed: {
    displayData() {
      if (this.dataKind === 'transition') {
        return {
          labels: this.chartData.map(d => {
            return d.label
          }),
          datasets: [
            {
              label: this.dataKind,
              data: this.chartData.map(d => {
                return d.transition
              }),
              backgroundColor: '#00B849',
              borderWidth: 0
            }
          ]
        }
      }
      return {
        labels: this.chartData.map(d => {
          return d.label
        }),
        datasets: [
          {
            label: this.dataKind,
            data: this.chartData.map(d => {
              return d.cummulative
            }),
            backgroundColor: '#00B849',
            borderWidth: 0
          }
        ]
      }
    }
  }
}
</script>
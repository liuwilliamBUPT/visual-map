<script setup lang="ts">
import CN from "../assets/100000_full.json";
import { onMounted } from "vue";
import * as echarts from "echarts/core";
import {
  TitleComponent,
  TitleComponentOption,
  ToolboxComponent,
  ToolboxComponentOption,
  TooltipComponent,
  TooltipComponentOption,
  VisualMapComponent,
  VisualMapComponentOption,
  GeoComponent,
  GeoComponentOption,
} from "echarts/components";
import { MapChart, MapSeriesOption } from "echarts/charts";
import { CanvasRenderer } from "echarts/renderers";

echarts.use([
  TitleComponent,
  ToolboxComponent,
  TooltipComponent,
  VisualMapComponent,
  GeoComponent,
  MapChart,
  CanvasRenderer,
]);

type EChartsOption = echarts.ComposeOption<
  | TitleComponentOption
  | ToolboxComponentOption
  | TooltipComponentOption
  | VisualMapComponentOption
  | GeoComponentOption
  | MapSeriesOption
>;

let chartDom = document.getElementById("main")!;
let myChart = echarts.init(chartDom);
let option: EChartsOption;

myChart.showLoading();

onMounted(() => {
  myChart.hideLoading();
  echarts.registerMap("CN", CN as any, {});

  option = {
    title: {
      text: "USA Population Estimates (2012)",
      subtext: "Data from www.census.gov",
      sublink: "http://www.census.gov/popest/data/datasets.html",
      left: "right",
    },
    tooltip: {
      trigger: "item",
      showDelay: 0,
      transitionDuration: 0.2,
    },
    visualMap: {
      left: "right",
      min: 500000,
      max: 38000000,
      inRange: {
        color: [
          "#313695",
          "#4575b4",
          "#74add1",
          "#abd9e9",
          "#e0f3f8",
          "#ffffbf",
          "#fee090",
          "#fdae61",
          "#f46d43",
          "#d73027",
          "#a50026",
        ],
      },
      text: ["High", "Low"],
      calculable: true,
    },
    toolbox: {
      show: true,
      //orient: 'vertical',
      left: "left",
      top: "top",
      feature: {
        dataView: { readOnly: false },
        restore: {},
        saveAsImage: {},
      },
    },
    series: [
      {
        name: "USA PopEstimates",
        type: "map",
        roam: true,
        map: "CN",
        emphasis: {
          label: {
            show: true,
          },
        },
        data: [{ name: "北京市", value: 4822023 }],
      },
    ],
  };

  myChart.setOption(option);

  option && myChart.setOption(option);
});
</script>

<template>
  <div id="main"></div>
</template>

<style scoped>
#main {
  height: 1000px;
  width: 1000px;
}
</style>

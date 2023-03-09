<template>
  <div class="home-container">
    <z-row :gutter="15">
      <z-col :span="7">
        <div class="echartList">
          <div class="chart-item">
            <box-container :boxTitle="systemStreamChartTitle">
              <system-stream-chart />
            </box-container>
          </div>
          <div class="chart-item">
            <box-container :boxTitle="systemSizeTopChartTitle">
              <streamSizeTopChart />
            </box-container>
          </div>
          <div class="chart-item">
            <box-container :boxTitle="year + '年销售品牌占比'">
              <word-chart />
            </box-container>
          </div>
        </div>
      </z-col>
      <z-col :span="10">
        <count-to :value="sum" suffix="万" :speed="20" />
        <div style="width:100%;height:85%">
          <scatter-map />
        </div>
      </z-col>
      <z-col :span="7">
        <div class="echartList">
          <div class="chart-item">
            <box-container :boxTitle="year + '年客户年龄分布'">
              <funnel-chart />
            </box-container>
          </div>
          <div class="chart-item">
            <box-container :boxTitle="year + '年公司市值'">
              <liquid-chart />
            </box-container>
          </div>
          <div class="chart-item">
            <box-container :boxTitle="year + '年同行业销售额度对比'">
              <line-chart />
            </box-container>
          </div>
        </div>
      </z-col>
    </z-row>
  </div>
</template>

<script>
import { ZRow, ZCol } from "@UI/components";
import boxContainer from "@/components/boxContainer/index";
import fourAngel from "@/components/fourAngel/index";
import countTo from "@/components/countTo/index";
import {
  cityCount,
  typeCount,
  scatterMap,
  wordChart,
  funnelChart,
  lineChart,
  liquidChart,
} from "./components";
import useResize from "@/componentApi/useResize.js";
import { ref } from "vue";
import SystemStreamChart from "@/views/homepage/components/systemStreamChart.vue";

import streamSizeTopChart from "@/views/homepage/components/streamSizeTopChart.vue";

export default {
  name: "homepage",
  components: {
    SystemStreamChart,
    streamSizeTopChart,
    ZRow,
    ZCol,
    boxContainer,
    cityCount,
    typeCount,
    scatterMap,
    wordChart,
    funnelChart,
    lineChart,
    liquidChart,
    fourAngel,
    countTo,
  },
  setup(props, context) {
    const systemStreamChartTitle= ref("新一代组件当日实时采集统计")
    const systemSizeTopChartTitle= ref("当日采集数据量TOP10")
    const { year, sum } = useResize();

    return {
      systemStreamChartTitle,
      systemSizeTopChartTitle,
      year,
      sum,
    };
  },
};
</script>

<style lang="scss" scoped>
.home-container {
  width: 100%;
  height: 100%;
  position: relative;

  .echartList {
    width: 100%;
    height: 100%;
    display: flex;
    flex-wrap: wrap;
    align-content: space-between;

    .chart-item {
      height: 32.1%;
      width: 100%;
    }
  }
}
</style>

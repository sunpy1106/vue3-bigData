<template>
  <div class="chart-wrapper" ref="streamSizeTopChart"></div>
</template>

<script>
import echarts from "echarts";
import { onMounted, ref } from "vue";
import { getSizeTop10Daily } from "@/api/mockChart";



export default {
  name: "streamSizeTopChart",
  setup() {
    const streamSizeTopChart = ref(null);
    let myChart = ref(null);


    onMounted(() => {
      getStreamSizeTop10();
    }
    );

    //模拟接口，获取echarts数据
    const getStreamSizeTop10 = async () => {
      const { data } = await getSizeTop10Daily({
      });
      initEcharts(data);
    };

    //渲染echarts图
    const initEcharts = (data) => {
      myChart = echarts.init(streamSizeTopChart.value);
      myChart.setOption(
        {
          grid: {
            left: "13%",
            right: "8%",
            bottom: "20%",
            top: "19%",
          },
          title: {
            show: data.length === 0,
            top: "center",
            left: "center",
            text: "暂无数据",
            textStyle: {
              color: "rgb(179, 239, 255)",
              fontSize: 12,
            },
          },
          tooltip: {
            trigger: "axis",
            axisPointer: {
              type: "line",
            },
          },
          toolbox: {
            feature: {
              dataView: {
                show: false,
              },
              magicType: {
                show: true,
                type: ["line", "bar"],
              },
              restore: {
                show: false,
              },

            },
            iconStyle: {
              normal: {
                borderColor: "#1990DA",
              },
            },
            top: 0,
            right: 5,
          },
          dataZoom: [
            {
              type: "inside",
              startValue: 0,
              endValue: 12,
            },
          ],
          legend: {
            show: true,
            left: "15",
            top: "0",
            itemWidth: 15,
            itemHeight: 11,
            textStyle: {
              color: "#00a9fb",
            },
          },
          xAxis: {
            type: "category",
            axisLine: {
              lineStyle: {
                color: "#397cbc",
              },
            },
            splitLine: {
              show: false,
            },
            axisTick: {
              show: false,
            },
            axisLabel: {
              show: true,
              textStyle: {
                color: "#cecece",
                fontSize: 12,
              },
              rotate: 15,
            },
            data: data.map((item) => item.name),
          },
          yAxis: [
            {
              type: "value",
              axisTick: {
                show: false,
              },
              axisLabel: {
                textStyle: {
                  fontSize: 12,
                  color: "#cecece",
                },
              },
              axisLine: {
                lineStyle: {
                  color: "#397cbc",
                },
              },
              //网格线
              splitLine: {
                lineStyle: {
                  color: "#11366e",
                },
              },
            },
          ],
          series: [
            {
              
              type: "bar",
              data: data.map((item) => item.value),

              barWidth: "10",
              barGap: "30%",
              itemStyle: {
                color: "#0F84CC",
              },
              lineStyle: {
                normal: {
                  width: 2,
                  color: "#0F84CC", // 线条颜色
                },
                borderColor: "#f0f",
              },
            },
          ],
        },
        true
      );
      myChart.off("click");
      myChart.getZr().off("click");
      myChart.getZr().on("click", (params) => {
        const pointInPixel = [params.offsetX, params.offsetY];
        if (myChart.containPixel("grid", pointInPixel) || data.length === 0) {
          //routerChange("/more");
        }
      });
    };

    const timer = setInterval(() => {
      getStreamSizeTop10()

    }, 2000)

    return {
      streamSizeTopChart,
    };
  },
};
</script>

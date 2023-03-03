<template>
  <!-- 
以下四块内容平均分布填满父容器,白色字体
新一代组件数量: 78
接入数据总大小：13412421423423
接入数据记录数：3542345
峰值TPS：2324
  -->
  <div class="flex flex-col justify-evenly text-yellow-400 font-mono">
    <div class="grid grid-cols-2  items-center justify-start mt-1 ">
      <div class="flex flex-col justify-center items-center  ">
        <span class="font-bold text-xl">新一代组件数量</span>
        <span id="systemcount">{{newComponentCount}}</span>
      </div>
      <div class="flex flex-col justify-center items-center">
        <span class="font-bold text-xl">接入数据总大小</span>
        <span>{{dataTotalSize}}</span>
      </div>
    </div>
    <div class="grid grid-cols-2  justify-start items-center mt-16 ">
      <div class="flex flex-col justify-center items-center">  
        <span class=" font-bold text-xl">峰值TPS</span>
        <span>{{dataRecordCount}}</span>
      </div>
      <div class="flex flex-col justify-center items-center">
        <span class="  font-bold text-xl">接入数据记录数</span>
        <span>{{ peakTPS }}</span>
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, watch } from 'vue'

import {getSystemData} from '@/api/mockChart'
// 定义四个变量，分别对应四个数据 
const newComponentCount=ref(null)
const dataTotalSize=ref(null)
const dataRecordCount=ref(null)
const peakTPS=ref(null)


//在mount时初始化四个变量的值
onBeforeUnmount(()=>{
  let { newComponentCount1, dataTotalSize1, dataRecordCount1, peakTPS1 } = getSystemData()
  //更新页面上的数据
  newComponentCount.value=newComponentCount1
  dataTotalSize.value=dataTotalSize1
  dataRecordCount.value=dataRecordCount1
  peakTPS.value=peakTPS1
  //打印变量的值
  console.log('newComponentCount1',newComponentCount1)
  console.log('dataTotalSize1',dataTotalSize1)
  console.log('dataRecordCount1',dataRecordCount1)
  console.log('peakTPS1',peakTPS1)

})

// 同时监听四个变量的变化，当变化时，更新页面上的数据
watch([newComponentCount,dataTotalSize,dataRecordCount,peakTPS],()=>{
  //调用mock方法获取四个变量最新的数据
  let { newComponentCount1, dataTotalSize1, dataRecordCount1, peakTPS1 } = getSystemData()
  //更新页面上的数据
  newComponentCount.value=newComponentCount1
  dataTotalSize.value=dataTotalSize1
  dataRecordCount.value=dataRecordCount1
  peakTPS.value=peakTPS1
  //打印日志
  console.log('newComponentCount1',newComponentCount1)
  console.log('dataTotalSize1',dataTotalSize1)
  console.log('dataRecordCount1',dataRecordCount1)
  console.log('peakTPS1',peakTPS1)
})
//打印日志
console.log('newComponentCount',newComponentCount.value)


</script>

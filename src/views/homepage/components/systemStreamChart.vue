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
import { get } from 'http';
import { randomInt } from 'crypto';
// 定义四个变量，分别对应四个数据 
let newComponentCount=ref(0)
let dataTotalSize=ref(0)
let dataRecordCount=ref(0)
let peakTPS=ref(0)


// 定义一个方法，用于获取四个变量的最新数据
const getSystemDataNew=async ()=>{
  const res= await getSystemData()
  newComponentCount.value= res.data.newComponentCount
  dataTotalSize.value= res.data.dataTotalSize
  dataRecordCount.value= res.data.dataRecordCount
  peakTPS.value= res.data.peakTPS
}



// 定义一个定时器，每隔一秒，获取四个变量的最新数据，并在页面上显示最新的值
const timer=setInterval(()=>{
  getSystemDataNew()

},2000)


</script>

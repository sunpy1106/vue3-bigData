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
        <span>78</span>
      </div>
      <div class="flex flex-col justify-center items-center">
        <span class="font-bold text-xl">接入数据总大小</span>
        <span>13412421423423</span>
      </div>
    </div>
    <div class="grid grid-cols-2  justify-start items-center mt-16 ">
      <div class="flex flex-col justify-center items-center">  
        <span class=" font-bold text-xl">峰值TPS</span>
        <span>2324</span>
      </div>
      <div class="flex flex-col justify-center items-center">
        <span class="  font-bold text-xl">接入数据记录数</span>
        <span>3542345</span>
      </div>
    </div>

  </div>
</template>

<script setup>

</script>

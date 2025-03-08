<template>
  <div id="clock">
    <div class="container">
      <div class="point"></div>
      <div class="hour"></div>
      <div class="minute"></div>
      <div class="second"></div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
let hour = ref(null);
let minute = ref(null);
let second = ref(null);
let deg = 0;

onMounted(() => {
  //获取元素
  hour.value = document.querySelector(".hour");
  minute.value = document.querySelector(".minute");
  second.value = document.querySelector(".second");

  //旋转函数
  const rotate = () => {
    let time = new Date();
    // 计算时分秒对应的角度
    let hoursDegress =
      ((time.getHours() * 3600 + time.getMinutes() * 60 + time.getSeconds()) /
        43200) *
      360;
    let minutesDegress =
      ((time.getMinutes() * 60 + time.getSeconds()) / 3600) * 360;
    let secondsDegress = (time.getSeconds() / 60) * 360;
    // 旋转
    hour.value.style.transform = `rotate(${hoursDegress}deg)`;
    minute.value.style.transform = `rotate(${minutesDegress}deg)`;
    second.value.style.transform = `rotate(${secondsDegress}deg)`;
    // 每时每刻旋转一次
    requestAnimationFrame(rotate);
  };
  rotate();
});
</script>

<style scoped>
#clock {
  width: 190px;
  height: 190px;
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  border: 2px solid white;
  position: relative;
  left: 100px;
  top: 100px;
  /* 发光效果 */
  box-shadow: 0 0 15px rgba(220, 220, 152, 0.5);
}
.point {
  background-color: white;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  position: relative;
  z-index: 100;
}
/* 调整指针的位置 */
.hour {
  background-color: rgb(194, 193, 193);
  width: 8px;
  height: 38.2px;
  position: absolute;
  z-index: 0;
  top: 55px;
  left: 91px;
  transform-origin: 50% 100%;
}
.minute {
  background-color: rgb(218, 217, 217);
  width: 5px;
  height: 61.8px;
  position: absolute;
  top: 33px;
  left: 92.5px;
  z-index: 10;
  transform-origin: 50% 100%;
}
.second {
  background-color: rgb(229, 113, 113);
  width: 3px;
  height: 90px;
  position: absolute;
  top: 5px;
  left: 93.5px;
  z-index: 20;
  transform-origin: 50% 100%;
}
</style>

<template>
    <div id="container">
        <!-- 动态渲染 -->
        <span class="const">const</span> <span class="name">currentTime</span> = <span class="signal">{</span><br>
            &emsp;&emsp;<span class="key">year</span>: <span class="num">{{ year }}</span><br>
            &emsp;&emsp;<span class="key">month</span>: <span class="num">{{ month }}</span><br>
            &emsp;&emsp;<span class="key">day</span>: <span class="num">{{ day }}</span><br>
            &emsp;&emsp;<span class="key">dayOfWeek</span>: <span class="str">"{{ dayOfWeek }}"</span><br>
            &emsp;&emsp;<span class="key">hour</span>: <span class="num">{{ hour }}</span><br>
            &emsp;&emsp;<span class="key">minute</span>: <span class="num">{{ minute }}</span><br>
            &emsp;&emsp;<span class="key">sencond</span>: <span class="num">{{ sencond }}</span><br>
            &emsp;&emsp;<span class="key">dayProgress</span>: <span class="num">{{ progress }}%</span><br>
        <span class="signal">}</span>;
    </div>
</template>

<script setup>
import { ref } from 'vue';
// 创建响应式对象
let year = ref();
let month = ref();
let day = ref();
let dayOfWeek = ref();
let hour  = ref();
let minute = ref();
let sencond = ref();
let progress = ref();
const init = ()=>{
    //每秒更新一次
    requestAnimationFrame(init)
    var options = { weekday: "long" };
    let time = new Date();
    //赋值
    year.value = time.getFullYear();
    month.value = (time.getMonth() + 1) > 9 ? (time.getMonth() + 1):'0'+(time.getMonth() + 1);
    day.value = (time.getDate()) > 9 ? (time.getDate()):'0'+(time.getDate());
    dayOfWeek.value = (new Intl.DateTimeFormat("en-US", options).format(time));
    hour.value  = (time.getHours() ) > 9 ? (time.getHours() ):'0'+(time.getHours() );
    minute.value = (time.getMinutes() ) > 9 ? (time.getMinutes() ):'0'+(time.getMinutes() );
    sencond.value = (time.getSeconds() ) > 9 ? (time.getSeconds() ):'0'+(time.getSeconds() );
    progress.value = ((time.getSeconds() + time.getMinutes()*60 + time.getHours()*3600)/86400*100).toFixed(2);
}
init();

</script>

<style  scoped>
.const{
    color: #5681a2;
}
.name{
    color:#55b7e7
}
.key{
    color: #9ed3eb;
}
.num{
    color:#a4b894
}
.str{
    color: #c18a71;
}
.signal{
    color: #f0cc1c;
}
.container{
    color: white;
}
</style>
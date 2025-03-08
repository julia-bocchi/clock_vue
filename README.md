# clck

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

# App主体
有两个组件和一个按钮切换主题
![[./img/Pasted image 20250308224017.png]]
# Text
通过动态渲染一个js对象在主页里
通过Date这个内置对象获取时间
```js
year.value = time.getFullYear();

    month.value = (time.getMonth() + 1) > 9 ? (time.getMonth() + 1):'0'+(time.getMonth() + 1);

    day.value = (time.getDate()) > 9 ? (time.getDate()):'0'+(time.getDate());

    dayOfWeek.value = (new Intl.DateTimeFormat("en-US", options).format(time));

    hour.value  = (time.getHours() ) > 9 ? (time.getHours() ):'0'+(time.getHours() );

    minute.value = (time.getMinutes() ) > 9 ? (time.getMinutes() ):'0'+(time.getMinutes() );

    sencond.value = (time.getSeconds() ) > 9 ? (time.getSeconds() ):'0'+(time.getSeconds() );

    progress.value = ((time.getSeconds() + time.getMinutes()*60 + time.getHours()*3600)/86400*100).toFixed(2);
```
调用requestAnimationFrame实现每秒渲染一次
```js
requestAnimationFrame(init)
```
# Clock
clock组件有三个指针
通过简单的计算公式得出每个指针的旋转角度（但还要蠢蛋竟然连时针转一圈为12小时这个事情都能忘😓）
```js
let hoursDegress =

      ((time.getHours() * 3600 + time.getMinutes() * 60 + time.getSeconds()) /

        1) *

      360;

    let minutesDegress =

      ((time.getMinutes() * 60 + time.getSeconds()) / 3600) * 360;

    let secondsDegress = (time.getSeconds() / 60) * 360;
```
再通过requestAnimationFrame每时每刻渲染同时优化性能。
```js
requestAnimationFrame(rotate);
```
记得要调用一次才行哦！


这里多提一嘴，如果用间隔器的话因为事件机制会导致有个先后顺序以前以后，比如先更新文字，再转到指针，导致效果不好
最终效果如下
![[./img/e0cbc9e41a981b7f0cd27fdeb02b942.png]]

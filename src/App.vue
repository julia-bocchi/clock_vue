<script>
import Text from "./components/text.vue";
import clock from "./components/clock.vue";
export default {
  components: {
    Text,
    clock,
  },
  setup() {
    const toggleTheme = () => {
      const container = document.querySelector(".toggle-container");
      container.classList.toggle("active");

      document.querySelector("body").style.backgroundColor =
        container.classList.contains("active")
          ? "rgb(244, 238, 228)"
          : "rgb(42, 38, 38)";
      document.querySelector("#container").style.color =
        container.classList.contains("active") ? "black" : "white";
      document.querySelector("#clock").style.borderColor =
        container.classList.contains("active") ? "black" : "white";
      document.querySelector("#clock").style.boxShow =
        container.classList.contains("active") ? "0 0 15px rgba(240, 177, 41, 0.5)" : "0 0 15px rgba(220, 220, 152, 0.5)";
    };
    return {
      toggleTheme,
    };
  },
};
</script>

<template>
  <div class="toggle-container" @click="toggleTheme">
    <div class="toggle-button"></div>
  </div>
  <Text></Text>
  <clock></clock>
</template>

<style scoped>
.toggle-container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  top: 0;
  right: 0;
}

.toggle-button {
  position: relative;
  width: 60px;
  height: 30px;
  background-color: #3498db;
  border-radius: 15px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.toggle-button::before {
  content: "";
  position: absolute;
  width: 26px;
  height: 26px;
  background-color: #ecf0f1;
  border-radius: 50%;
  top: 2px;
  left: 2px;
  transition: transform 0.3s;
}

.toggle-container.active .toggle-button {
  background-color: rgb(244, 244, 134);
}

.toggle-container.active .toggle-button::before {
  transform: translateX(30px);
}
</style>

<template>
  <div class="weather-box">
    <div class="weather-box-item">
      <div class="weather-box-item-date">
        <p>{{ fullDate }}</p>
      </div>
      <div class="weather-box-item-icon">
        <img src="../assets/day.svg" alt="weather" />
      </div>
      <div class="weather-box-item-info">
        <h3 class="info">Its cloudy</h3>
        <div class="celsius">29 <sup>o</sup></div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { getDate } from "../utils/date";

export default defineComponent({
  name: "WeatherBox",
  props: {
    type: String,
  },
  setup() {
    const fullDate = ref<string>(getDate());

    return {
      fullDate,
    };
  },
});
</script>

<style lang="less" scoped>
.displayFlex(@x: center, @y: center) {
  display: flex;
  justify-content: @x;
  align-items: @y;
}
.weather-box {
  min-height: 85vh;
  .displayFlex();
  color: #f1f1f1;
  .weather-box-item {
    max-width: 550px;
    width: 100%;
    height: 80vh;
    display: flex;
    flex-direction: column;
    border-radius: 17px;
    background-color: rgba(255, 255, 255, 0.06);
    border: 1px solid rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(30px);
    .weather-box-item-date {
      flex: 0.2;
      .displayFlex();
      p {
        font-size: 0.9rem;
        font-weight: 300;
      }
    }
    .weather-box-item-icon {
      flex: 1;
      .displayFlex();
      img {
        width: 250px;
        height: 250px;
      }
    }
    .weather-box-item-info {
      flex: 1;
      .displayFlex(space-evenly, center);
      flex-direction: column;
      .info {
        font-size: 1.5rem;
        padding: 0.5rem;
        border-radius: 5px;
      }
      .celsius {
        font-size: 3rem;
        font-weight: 700;
      }
    }
  }
}
</style>

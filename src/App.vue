<template>
  <div class="input-wrapper">
    <div class="form__group field">
      <input
        type="input"
        class="form__field"
        placeholder="Search for a city"
        name="name"
        id="name"
        v-model="input"
        @keypress="fetchWeather"
        required
      />
      <label for="name" class="form__label">Search for a city</label>
    </div>
  </div>
  <WeatherBox v-if="typeof weather.main != 'undefined'" :weather="weather" />
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import WeatherBox from "./components/WeatherBox.vue";
import { Weather } from "./types/index";

export default defineComponent({
  name: "App",
  components: {
    WeatherBox,
  },
  setup() {
    const input = ref<string>("");
    const apiKey = ref<string>(process.env.VUE_APP_API_KEY as string);
    const weather = ref<Weather>({
      name: "",
      country: "",
      temp: 0,
      main: "",
    });

    return {
      input,
      apiKey,
      weather,
    };
  },
  methods: {
    fetchWeather(e: KeyboardEvent) {
      if (e.key == "Enter" && this.input.trim() !== "") {
        fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.input}&units=imperial&APPID=${this.apiKey}`
        )
          .then((res) => res.json())
          .then((data) => {
            const {
              name,
              sys: { country },
              main: { temp },
              weather: [{ main }],
            } = data;

            this.getResults({ name, country, temp, main });
          })
          .catch((err) => {
            console.log(err);
          });
      }
    },
    getResults(results: Weather) {
      this.weather = results;
    },
  },
});
</script>

<style lang="less">
@white: #fff;
@gray: #9b9b9b;
@borderImage: linear-gradient(to top, #e6e9f0 0%, #eef1f5 100%);

.input-wrapper {
  min-height: 15vh;
  display: flex;
  justify-content: center;
  align-items: center;
  .form__group {
    position: relative;
    padding: 15px 0 0;
    width: 35%;
    @media screen and (max-width: 768px) {
      width: 80%;
    }
    .form__field {
      font-family: inherit;
      width: 100%;
      border: 0;
      border-bottom: 2px solid rgba(255, 255, 255, 0.1);
      outline: 0;
      font-size: 1.1rem;
      color: @white;
      padding: 7px 0;
      background: transparent;
      transition: border-color 0.2s;
      &::placeholder {
        color: transparent;
      }
      &:placeholder-shown ~ .form__label {
        font-size: 1.2rem;
        cursor: text;
        top: 21px;
      }
      &:focus {
        ~ .form__label {
          position: absolute;
          top: 0;
          display: block;
          transition: 0.2s;
          font-size: 1rem;
          color: @white;
          font-weight: 700;
        }
        padding-bottom: 6px;
        font-weight: 300;
        border-image: @borderImage;
        border-image-slice: 1;
      }
      &:required {
        box-shadow: none;
      }
      &:invalid {
        box-shadow: none;
      }
    }
    .form__label {
      position: absolute;
      top: 0;
      display: block;
      transition: 0.2s;
      font-size: 0.8rem;
      color: @gray;
    }
  }
}
</style>

<template>
    <div id="app" class="app">
        <img alt="Vue logo" src="./assets/logo.png">
        <div>
            <a class="task-link" target="_blank" href="https://kodaktor.ru/frmw_005">Задание FRMW-005</a>
        </div>
        <div class="aspect-ratio">
            <div class="aspect-ratio__inner">
                <div :style="style"></div>
            </div>
        </div>
        <div class="flex card bordered rounded">
            <div>
                <rgb-color-slider class="bordered-bottom" color="R" v-model="R" />
                <rgb-color-slider class="bordered-bottom" color="G" v-model="G" />
                <rgb-color-slider color="B" v-model="B" />
            </div>
        </div>
        <div class="author">Автор: <strong>Кочетыгов Андрей</strong></div>
    </div>
</template>

<script>
import './main.css'
import RgbColorSlider from './components/RgbColorSlider'
export default {
  name: 'App',
  components: { RgbColorSlider },
  data: () => ({
    R: 128,
    G: 128,
    B: 128,
  }),
  computed: {
    style () {
      return {
        width: `100%`,
        height: `100%`,
        background: `rgb(${this.R}, ${this.G}, ${this.B})`
      }
    }
  },
}
</script>

<style>
  body {
    margin: 0;
    background: #ebeced;
    display: flex;
    flex-direction: column;
    justify-content: stretch;
    align-items: center;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    min-height: 100vh;
    padding-bottom: 3rem;
    padding-top: 3rem;
  }

  .app {
      padding: 2rem;
  }

  .aspect-ratio {
      position: relative;
      padding-top: calc(16px / 9 * 100);
      width: 100%;
      margin-bottom: 1rem;
      border-radius: 4px;
      overflow: hidden;
  }

  .aspect-ratio__inner {
      position: absolute;
      left: 0;
      top: 0;
      bottom: 0;
      right: 0;
  }

  button {
    border-radius: 4px;
    border: 0;
    padding: 0.5rem 0.75rem;
    outline: none;
    color: #fff;
    background: #2c3e50;
    cursor: pointer;
  }

  .author {
    margin-top: 0.75rem;
  }

  .task-link {
    display: inline-block;
    margin-bottom: 0.75rem;
  }
</style>

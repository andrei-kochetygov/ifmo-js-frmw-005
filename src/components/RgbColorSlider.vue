<template>
    <div class="group flex">
        <div class="group-element">
            <label :for="id">{{ color }}</label>
        </div>
        <div class="divider-flex"></div>
        <div class="group-element">
            <div :style="colorSampleStyle"></div>
        </div>
        <div class="divider-flex"></div>
        <div class="group-element grow">
            <input class="full-width" :id="id" type="range" step="1" min="0" max="256" :value="val" @input="input">
        </div>
    </div>
</template>

<style scoped>
    .group {
        align-items: center;
    }
    .group-element {
        display: flex;
        flex-direction: column;
        justify-items: center;
        justify-content: center;
        padding: 0.75rem;
    }
    label {
        display: inline-block;
        margin: 0;
        width: 20px;
        text-align: center;
    }
    input {
        margin: 0;
    }
</style>

<script>
const normalize = (value) => {
  value = value > 255 ? 255 : value
  value = value < 0 ? 0 : value
  return value
}
export default {
  name: 'RgbColorSlider',
  props: {
    id: {
      type: String,
      default: null,
    },
    color: {
      type: String,
      required: true,
      validator(value) {
        return ['R', 'G', 'B'].includes(value)
      },
    },
    value: {
      type: Number,
      default: 128,
      validator(value) {
        return -1 < value && value < 256
      },
    }
  },
  data() {
    return {
      val: this.value,
    }
  },
  watch: {
    value(newValue) {
      this.val = newValue
    },
  },
  computed: {
    colorSampleStyle() {
      return {
        height: '20px',
        width: '20px',
        backgroundColor: this.cssRgbValue,
      }
    },
    cssRgbValue() {
      switch (this.color) {
        case 'R': return `rgb(${this.val}, 0, 0)`
        case 'G': return `rgb(0, ${this.val}, 0)`
        case 'B': return `rgb(0, 0, ${this.val})`
        default: return `rgb(0, 0, 0)`
      }
    },
  },
  methods: {
    input({ target }) {
      this.val = normalize(+target.value)
      this.$emit('input', this.val)
    },
  },
}
</script>

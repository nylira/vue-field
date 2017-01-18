<template>
  <textarea v-if="inputType === 'textarea'"
    class="inputClass"
    :value="inputValue"
    :placeholder="inputPlaceholder"
    v-bind:value="value"
    v-on:input="value = arguments[0]"
    >
  </textarea>
  <input v-else
    :class="inputClass"
    :value="inputValue"
    :placeholder="inputPlaceholder"
    v-bind:value="value"
    v-on:input="value = arguments[0]"
  >
</template>

<script>
export default {
  name: 'pz-button',
  computed: {
    inputClass () {
      let value = 'pz-input'
      if (this.inputSize === 'large') value += ' pz-input-large'
      if (this.inputSize === 'small') value += ' pz-input-small'
      if (this.inputStyle === 'tendermint') value += ' pz-style-tendermint'
      return value
    },
  },
  props: ['input-value', 'input-placeholder', 'input-type', 'input-size', 'input-style']
}
</script>

<style src="./style.css"></style>

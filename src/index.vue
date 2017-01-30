<template>
  <textarea v-if="inputType === 'textarea'"
    class="inputClass"
    :placeholder="inputPlaceholder"
    :value="value"
    @input="updateValue($event.target.value)"
    >
  </textarea>
  <input v-else
    :type="inputType"
    :class="inputClass"
    :placeholder="inputPlaceholder"
    :value="value"
    @input="updateValue($event.target.value)"
  >
</template>

<script>
export default {
  name: 'pz-input',
  computed: {
    inputClass () {
      let value = 'pz-input'
      if (this.inputSize === 'large') value += ' pz-input-large'
      if (this.inputSize === 'small') value += ' pz-input-small'
      if (this.inputStyle === 'tendermint') value += ' pz-style-tendermint'
      return value
    },
  },
  methods: {
    updateValue (value) {
      let formattedValue = value.trim()
      // Emit the number value through the input event
      this.$emit('input', formattedValue)
    }
  },
  mounted () {
    if (this.required) {
      this.$el.required = true
    }
  },
  props: ['input-placeholder', 'input-type', 'input-size', 'input-style', 'value', 'required']
}
</script>

<style src="./style.css"></style>

<template>
  <textarea v-if="type === 'textarea'"
    class="css"
    :placeholder="placeholder"
    :value="value"
    @input="updateValue($event.target.value)"
    >
  </textarea>
  <input v-else
    :type="type"
    :class="css"
    :placeholder="placeholder"
    :value="value"
    @input="updateValue($event.target.value)"
  >
</template>

<script>
export default {
  name: 'pz-input',
  computed: {
    css () {
      let value = 'pz-input'
      if (this.size === 'large') value += ' pz-input-large'
      if (this.size === 'small') value += ' pz-input-small'
      if (this.theme === 'tendermint') value += ' pz-style-tendermint'
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
  props: ['placeholder', 'type', 'size', 'value', 'required', 'theme']
}
</script>

<style src="./style.css"></style>

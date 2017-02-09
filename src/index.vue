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
  name: 'ni-input',
  computed: {
    css () {
      let value = 'ni-input'
      if (this.size === 'lg') value += ' ni-input-large'
      if (this.size === 'sm') value += ' ni-input-small'
      if (this.theme === 'tendermint') value += ' ni-theme-tendermint'
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
  beforeMount () {
    if (this.required) {
      this.$el.required = true
    }
  },
  mounted () {
    let el = this.$el
    if (this.type === 'number') {
      el.addEventListener('focus', function () {
        el.select()
      })
    }
  },
  props: ['placeholder', 'type', 'size', 'value', 'required', 'theme']
}
</script>

<style src="./style.css"></style>

<template>
  <div class="css" v-if="type === 'select'">
    <select 
      :class="css"
      :placeholder="placeholder"
      :value="value"
      @input="updateValue($event.target.value)">
    </select>
  </div>
  <textarea v-if="type === 'textarea'"
    :class="css"
    :placeholder="placeholder"
    :value="value"
    @input="updateValue($event.target.value)">
  </textarea>
  <input v-else
    :type="type"
    :class="css"
    :placeholder="placeholder"
    :value="value"
    @input="updateValue($event.target.value)">
  </input>
</template>

<script>
export default {
  name: 'ni-field',
  computed: {
    css () {
      let value = 'ni-field'
      if (this.size === 'lg') value += ' ni-field-large'
      if (this.size === 'sm') value += ' ni-field-small'
      if (this.theme === 'tendermint') value += ' ni-theme-tendermint'
      if (this.theme === 'cosmos') value += ' ni-theme-cosmos'
      return value
    }
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

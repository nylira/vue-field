<template>
  <div :class="css" v-if="type === 'select'">
    <select 
      :class="css"
      :placeholder="placeholder"
      :value="value"
      @input="updateValue($event.target.value)">
      <option v-for="option in options" :value="option.id">
        {{ option.id }}
      </option>
    </select>
  </div>
  <textarea v-else-if="type === 'textarea'"
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
  props: ['placeholder', 'type', 'size', 'value', 'theme', 'options'],
  computed: {
    css () {
      let value = 'ni-field'
      if (this.type === 'select') value += ' ni-field-select'
      if (this.size) value += ` ni-field-size-${this.size}`
      if (this.theme) value += ` ni-field-theme-${this.theme}`
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
  mounted () {
    let el = this.$el
    if (this.type === 'number') {
      el.addEventListener('focus', function () {
        el.select()
      })
    }
  }
}
</script>

<style src="./style.css"></style>

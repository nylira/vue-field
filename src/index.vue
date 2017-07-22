<template lang='pug'>
.ni-select(v-if="type === 'select' || type === 'countries'")
  select(
    :class='css'
    :placeholder='placeholder'
    :value='value'
    @input='updateValue($event.target.value)')

    option(v-if="type === 'countries'" v-for='countries in countries'
      :value='country.value')
      | {{ country.key }}
    option(v-if='options' v-for='option in options' :value='option.value')
      | {{ option.key }}
  .ni-field-select-addon(@click='toggleSelect')
    i.material-icons arrow_drop_down

textarea(v-else-if="type === 'textarea'"
  :class='css'
  :placeholder='placeholder'
  :value='value'
  @input='updateValue($event.target.value)')

input(v-else=''
  :type='type'
  :class='css'
  :placeholder='placeholder'
  :value='value'
  @input='updateValue($event.target.value)')
</template>

<script>
import countries from './countries.json'
export default {
  name: 'ni-field',
  props: ['placeholder', 'type', 'size', 'value', 'theme', 'options'],
  computed: {
    css () {
      let value = 'ni-field'
      if (this.type === 'select' || this.type === 'countries') {
        value += ' ni-field-select'
      }
      if (this.size) value += ` ni-field-size-${this.size}`
      if (this.theme) value += ` ni-field-theme-${this.theme}`
      return value
    }
  },
  data: () => ({
    countries: countries
  }),
  methods: {
    updateValue (value) {
      let formattedValue = value.trim()
      // Emit the number value through the input event
      this.$emit('input', formattedValue)
    },
    toggleSelect () {
      console.log('toggling select')
      let select = document.querySelector(this.$el.id + ' > select')
      console.log('select', select)
      select.click()
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

<style lang='stylus'>
sans = -apple-system, ".SFNSText-Regular", "San Francisco", "Roboto", "Segoe UI", "Helvetica Neue", "Lucida Grande", sans-serif

.ni-field
  -webkit-appearance none
  border 1px solid #ccc
  vertical-align top
  padding 0.1875rem 0.5rem
  font-size 16px
  line-height 1.5rem
  border-radius 0
  display block
  width 100%
  min-width 0
  background #fff

.ni-field:disabled
  color #666
  text-shadow none
  box-shadow none
  background #eee

.ni-field:focus
  outline none
  box-shadow none
  border 1px solid #09c

input.ni-field
  height 2rem

textarea.ni-field
  height 4rem
  resize vertical

.ni-select
  display flex

  select
    flex 1
    appearance none
    border-radius 0
    background #fff
    width auto

  .ni-field-select-addon
    flex 0 0 2rem
    display flex
    align-items center
    justify-content center
    box-sizing border-box
    height 2rem
    border 1px solid #ccc
    border-left none

    background #fff
    text-align center
    color #000
    pointer-events none

/*==============================================================================*/
.input-group-addon
  background #eee
  border 1px solid #ccc
  border-left none
  padding 0 0.5rem
  color #666
  line-height 1.875rem
  font-size 0.75rem

@media screen and (min-width 360px)
  .input-group-addon
    font-size 1rem

/*==============================================================================*/
/* WebKit, Blink, Edge */
.ni-field::-webkit-input-placeholder
  color #666

/* Mozilla Firefox 4 to 18 */
.ni-field:-moz-placeholder
  color #666
  opacity 1

/* Mozilla Firefox 19+ */
.ni-field::-moz-placeholder
  color #666
  opacity 1

/* Internet Explorer 10-11 */
.ni-field:-ms-input-placeholder
  color #666

/* Standard (https//drafts.csswg.org/selectors-4/#placeholder) */
.ni-field:placeholder-shown
  color #666

/*==============================================================================*/
/* sizes */
.ni-field.ni-field-size-sm
  height 1.5rem
  font-size 0.75rem
  padding-left 0.5rem
  padding-right 0.5rem

.ni-field.ni-field-size-lg
  height 3rem
  font-size 1.125rem
  padding-left 0.75rem
  padding-right 0.75rem

/*==============================================================================*/
/* tendermint styles */
.ni-field.ni-field-theme-tendermint
  color #fff
  background hsl(210,70%,18%)
  border-color hsl(210,70%,38%)

.ni-field.ni-field-theme-tendermint:focus
  border-color hsl(210,70%,43%)

.ni-field.ni-field-theme-tendermint::-webkit-input-placeholder
  color hsl(210,70%,70%)

/* Mozilla Firefox 4 to 18 */
.ni-field.ni-field-theme-tendermint:-moz-placeholder
  color hsl(210,70%,70%)
  opacity 1

/* Mozilla Firefox 19+ */
.ni-field.ni-field-theme-tendermint::-moz-placeholder
  color hsl(210,70%,70%)
  opacity 1

/* Internet Explorer 10-11 */
.ni-field.ni-field-theme-tendermint:-ms-input-placeholder
  color hsl(210,70%,70%)

/* Standard (https//drafts.csswg.org/selectors-4/#placeholder) */
.ni-field.ni-field-theme-tendermint:placeholder-shown
  color hsl(210,70%,70%)

/*==============================================================================*/
/* cosmos styles */
.ni-field.ni-field-theme-cosmos
  background transparent
  color hsl(0,0%,70%)
  border-color hsl(210, 9%, 21%)
  font-family sans 

  &:hover
    border-color hsl(210, 7%, 29%)

  &:focus,
  &:active
    border-color hsl(210, 100%, 50%)
    color hsl(210, 4%, 91%)
    background hsl(0,0%,0%)

  &::-webkit-input-placeholder
    color hsl(0,0%,70%)

  /* Mozilla Firefox 4 to 18 */
  &:-moz-placeholder
    color hsl(0,0%,70%)
    opacity 1

  /* Mozilla Firefox 19+ */
  &::-moz-placeholder
    color hsl(0,0%,70%)
    opacity 1

  /* Internet Explorer 10-11 */
  &:-ms-input-placeholder
    color hsl(0,0%,70%)

  /* Standard (https//drafts.csswg.org/selectors-4/#placeholder) */
  &:placeholder-shown
    color hsl(0,0%,70%)
</style>

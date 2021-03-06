<template lang="pug">
.ni-select(v-if="type === 'select' || type === 'countries'")
  select(
    :class="css"
    :value="value"
    @input="updateValue($event.target.value)"
    @change="onChange"
    @keyup="onKeyup"
    @keydown="onKeydown")
    option(value="" disabled selected hidden) {{ selectPlaceholder }}
    option(v-if="options" v-for="i in options" :value="i.value") {{ i.key }}
    option(v-else-if="type === 'countries'" v-for="i in countries" :value="i.value"
    :key="i.key") {{ i.key }}
  .ni-field-select-addon: i.material-icons arrow_drop_down

// .ni-datetime(v-else-if="type === 'datetime'")
  input(
    type="text"
    :class="css"
    @change="onChange"
    @keyup="onKeyup"
    @keydown="onKeydown"
    :placeholder="placeholder"
    :value="value"
    @input="updateValue($event.target.value)")

textarea(v-else-if="type === 'textarea'"
  :class="css"
  @change="onChange"
  @keyup="onKeyup"
  @keydown="onKeydown"
  :placeholder="placeholder"
  :value="value"
  @input="updateValue($event.target.value)")

label.ni-toggle(
  v-else-if="type === 'toggle'"
  :class="toggleClass")
  .ni-toggle-wrapper
    span {{toggleLongerWord}}
    .toggle-option-checked: div {{toggleOptions.checked}}
    .toggle-option-unchecked: div {{toggleOptions.unchecked}}
    .toggle-handle
    input(
      type="checkbox"
      @change="onChange"
      :value="value"
    )

input(v-else
  :type="type"
  :class="css"
  @change="onChange"
  @keyup="onKeyup"
  @keydown="onKeydown"
  :placeholder="placeholder"
  :value="value"
  @input="updateValue($event.target.value)")
</template>

<script>
// import flatpickr from 'flatpickr'
import countries from "./countries.json";
export default {
  name: "ni-field",
  props: [
    "placeholder",
    "type",
    "size",
    "value",
    "theme",
    "options",
    "change",
    "keyup",
    "keydown",
    "options"
  ],
  computed: {
    css() {
      let value = "ni-field";
      if (this.type === "select" || this.type === "countries") {
        value += " ni-field-select";
      }
      if (this.type === "toggle") {
        value += " ni-field-toggle";
      }
      if (this.size) value += ` ni-field-size-${this.size}`;
      if (this.theme) value += ` ni-field-theme-${this.theme}`;
      return value;
    },
    toggleClass() {
      return {
        unchecked: !this.value
      };
    },
    toggleLongerWord() {
      return this.toggleOptions.checked.length >
        this.toggleOptions.unchecked.length
        ? this.toggleOptions.checked
        : this.toggleOptions.unchecked;
    },
    selectPlaceholder() {
      if (this.placeholder) return this.placeholder;
      else return "Select option...";
    },
    toggleOptions() {
      if (this.options && this.options.checked && this.options.unchecked)
        return this.options;
      return {
        checked: "on",
        unchecked: "off"
      };
    }
  },
  data: () => ({
    countries: countries
  }),
  methods: {
    toggle() {
      this.value = !this.value;
    },
    updateValue(value) {
      let formattedValue = value.trim();
      // Emit the number value through the input event
      this.$emit("input", formattedValue);
    },
    onChange(...args) {
      if (this.change) return this.change(...args);
    },
    onKeyup(...args) {
      if (this.keyup) return this.keyup(...args);
    },
    onKeydown(...args) {
      if (this.keydown) return this.keydown(...args);
    }
  },
  mounted() {
    let el = this.$el;
    if (this.type === "number") {
      el.addEventListener("focus", function() {
        el.select();
      });
    }
    /* if (this.type === 'datetime') {
      this.picker = flatpickr(el, {
        enableTime: true,
        dateFormat: 'Y-m-d H:i',
        onChange: (dateObj, dateStr) => this.updateValue(dateStr)
      })
      // console.log('its a datetime!', el)
    } */
  }
};
</script>

<style lang='stylus'>
@require '~variables'

.ni-field
  -webkit-appearance none

  border 1px solid var(--input-bc, #ccc)
  border-radius 0

  vertical-align top

  padding 0.1875rem 0.5rem

  display block
  width 100%
  min-width 0

  background var(--input-bg, #fff)

  color var(--txt, #333)
  font-size 16px
  line-height 1.5rem

.ni-field:disabled
  color var(--dim, #666)
  text-shadow none
  box-shadow none
  background var(--app-fg, #eee)
  border var(--app-fg, #eee)

.ni-field:focus
  outline none
  box-shadow none
  border 1px solid var(--link, #00f)

input.ni-field
  height 2rem

textarea.ni-field
  height 4rem
  resize vertical

.ni-toggle
  border 1px solid var(--input-bc, #ccc)
  height 2rem
  padding 0 2px
  border-radius 1rem
  *
    cursor pointer
  .ni-toggle-wrapper
    padding 0 1.25rem
    transform: rotate(0deg);
    margin-right calc(1.625rem / 2)
    margin-left calc(1.625rem / 2)
    &:before, &:after
      content ''
      width 1.625rem
      height 1.625rem
      position absolute
      top 2px
      z-index: 0
    &:before
      background var(--success, #4acf4a)
      border-radius 1em 0 0 1em
      left calc(-1.625rem / 2)
    &:after
      background var(--danger, #8c8fa6)
      border-radius 0 1em 1em 0
      right calc(-1.625rem / 2)
    .toggle-option-checked,
    .toggle-option-unchecked
      z-index: 1
      position absolute
      top 2px
      overflow hidden
      height 1.625rem
      clip: rect(0, auto, auto, 0);
      transition width 500ms ease
      > div
        position fixed
        left 0
        width 100%
        top 2px
        text-align center
    .toggle-option-checked
      background: var(--success, #4acf4a)
      left 0
      width 100%
    .toggle-option-unchecked
      background: var(--danger, #8c8fa6)
      right 0
      width 0%
    .toggle-handle
      &:after
        transition right 500ms ease, left 500ms ease
        position absolute
        top 2px
        right calc(-1.65rem/2)
        left auto
        width 1.625rem
        height 1.625rem
        background var(--bc, #d4d5de)
        border-radius 1rem
        z-index z(listItem)

        // display flex
        // align-items center
        // justify-content center
        content ''
        // content 'drag_handle'
        // font-size x
        // font-family 'Material Icons'
        // transform  rotate(90DEG)
        // color var(--bc, hsl(233, 22%, 23%))
    input[type="checkbox"]
      display none
  &.unchecked
    .toggle-option-checked
      width 0
    .toggle-option-unchecked
      width 100%
    .toggle-handle:after
      right calc(100% - .7500rem)

.ni-select
  position relative

  select
    appearance none
    border-radius 0
    background var(--input-bg, #fff)
    width 100%
    color var(--txt, #333)
    padding-right 2rem

    &:invalid
      color dim

    option
      color txt
      background var(--input-bg, #fff)
      font-family sans
      &:checked
        color var(--bright, #000)
        background var(--hover-bg, #ccf)

  .ni-field-select-addon
    position absolute
    top 0
    right 0

    display flex
    align-items center
    justify-content center
    box-sizing border-box
    height 2rem
    width 2rem
    border-left 1px solid var(--input-bc, #ccc)

    background var(--input-bg, #fff)
    text-align center
    color var(--txt, #333)
    pointer-events none

/*==============================================================================*/

.ni-datetime
  position relative

.ni-datetime:after
  display flex
  align-items center
  justify-content center
  box-sizing border-box
  width 2rem
  height 2rem
  position absolute
  top 0
  right 0
  border 1px solid var(--input-bc, #ccc)
  background var(--app-bg, #fff)
  font-family FontAwesome
  content "\f073"
  text-align center
  color var(--bright)
  pointer-events none

/*==============================================================================*/

.input-group-addon
  background var(--input-bg, #fff)
  border 1px solid var(--input-bc, #ccc)
  border-left none
  padding 0 0.5rem
  color var(--txt, #333)
  line-height 1.875rem
  font-size 0.75rem

@media screen and (min-width 360px)
  .input-group-addon
    font-size 1rem

/*==============================================================================*/
/* WebKit, Blink, Edge */

.ni-field::-webkit-input-placeholder
  color var(--dim, #666)

/* Mozilla Firefox 4 to 18 */
.ni-field:-moz-placeholder
  color var(--dim, #666)
  opacity 1

/* Mozilla Firefox 19+ */
.ni-field::-moz-placeholder
  color var(--dim, #666)
  opacity 1

/* Internet Explorer 10-11 */
.ni-field:-ms-input-placeholder
  color var(--dim, #666)

/* Standard (https//drafts.csswg.org/selectors-4/#placeholder) */
.ni-field:placeholder-shown
  color var(--dim, #666)

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
</style>

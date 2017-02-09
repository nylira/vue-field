# vue-input
Flexible input field component for Vue 2.

## Installation

    npm install @nylira/vue-input

## Usage

    <template>
      <field date="February 28, 2017"></field>
    </template>

    <script>
      import Field from '@nylira/vue-input'
      export default {
        components: {
          Field
        }
      }
    </script>

    <style>
      .ni-field {
        width: 320px;
      }
    </style>

## Props

  props: ['placeholder', 'type', 'size', 'value', 'required', 'theme']

    value=""
    // The value of the input field
    // Options: Any valid string

    placeholder=""
    // The input field placeholder
    // Options: Any valid string

    size=""
    // Chanage the size of the input field
    // Options: "lg", "sm"

    required
    // Self-explanatory

    theme="tendermint"
    // Adds a custom input field theme
    // Options: "tendermint"

    type="text"
    // Input field type (mainly used for HTML forms)
    // Options: "text", "email", "tel", "num", "password", "textarea"

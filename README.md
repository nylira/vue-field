# vue-input
Flexible input field component for Vue 2.

## Installation

    npm install @nylira/vue-input

## Usage

    <template>
      <field v-model="email" placeholder="Enter your email"></field>
    </template>

    <script>
      import Field from '@nylira/vue-input'
      export default {
        components: {
          Field
        },
        data () {
          return {
            email: ''
          }
        }
      }
    </script>

    <style>
      .ni-field {
        width: 320px;
      }
    </style>

## Props

    value=""
    // The value of the input field, also can be used with v-model
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

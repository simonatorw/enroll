<template>
  <v-stepper v-model="e1">
    <v-stepper-header>
      <v-stepper-step :complete="e1 > 1" step="1">Confirm Identity</v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step :complete="e1 > 2" step="2">Coverage</v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step step="3">Scheduling</v-stepper-step>
    </v-stepper-header>

    <v-stepper-items>
      <v-stepper-content step="1">
        <v-card
          class="mb-2 confirm"
          color="lighten-1"
        >
          <h1>Please confirm you identity</h1>
          <v-form ref="form" v-model="valid" lazy-validation>
            <div class="formContainer">
              <div class="formCol">
                <v-text-field
                  v-model="firstName"
                  label="First Name"
                  disabled
                ></v-text-field>
                <v-text-field
                  v-model="dob"
                  :rules="dobRules"
                  label="Date of Birth"
                  placeholder="MM-DD-YYYY"
                  hint="Enter your Date of Birth here"
                  persistent-hint
                  required
                ></v-text-field>
                <v-text-field
                  v-model="preferredNumber"
                  :rules="numberRules"
                  label="Preferred Number"
                  placeholder="XXX-XXX-XXXX"
                  required
                ></v-text-field>
              </div>
              <div class="formCol">
                <v-text-field
                  v-model="lastName"
                  label="Last Name"
                  disabled
                ></v-text-field>
                <v-text-field
                  v-model="email"
                  label="Email"
                  disabled
                ></v-text-field>
                <v-select
                  v-model="phoneType"
                  :items="items"
                  label="Phone Type"
                  required
                ></v-select>
              </div>              
            </div>
          <div class="button-bar">
            <v-btn
              color="primary"
              @click="e1 = 2"
              :disabled="!isComplete"
            >
              Confirm Identity
            </v-btn>
          </div>
          </v-form>
        </v-card>
      </v-stepper-content>

      <v-stepper-content step="2">
        <v-card
          class="mb-2 confirm"
          color="lighten-1"
        >
          <v-icon large class="checkmark">checkmark</v-icon>
          <div class="confirm-msg">
            Great! You're covered for 8 weeks of treatment with AbleTo at no cost to you.<sup>*</sup>
          </div>  
          <v-btn
            color="primary"
            @click="e1 = 3"
          >
            Schedule First Consultation
          </v-btn>
        </v-card>
        <div class="footnote">
          <sup>*</sup>Comment comment comment
        </div>
      </v-stepper-content>

      <v-stepper-content step="3">
        <v-card
          class="mb-5"
          color="grey lighten-1"
          height="200px"
        ></v-card>
      </v-stepper-content>
    </v-stepper-items>
  </v-stepper>
</template>

<script>
  export default {
    data () {
      return {
        e1: 0,
        valid: true,
        firstName: 'Johnny',
        lastName: 'Smith',
        dob: '',
        dobRules: [
          v => !!v || 'Date of Birth is required',
          v => (/^((0|1)\d{1})-((0|1|2)\d{1})-((19|20)\d{2})/g).test(v) || 'Date of Birth must be valid'
        ],
        email: 'john.smith@email.com',
        preferredNumber: '',
        numberRules: [
          v => !!v || 'Preferred number is required',
          v => (/^(?:\(\d{3}\)?\s|\d{3}-)\d{3}-\d{4}$/).test(v) || 'Preferred number must be valid'
        ],
        phoneType: '',
        items: [
          'Mobile',
          'Home',
          'Work'
        ]
      }
    },
    computed: {
      isComplete() {
        return this.dob && this.preferredNumber && this.phoneType && this.fields.dob.validated && this.fields.preferredNumber.validated && this.fields.phoneType.validated;
      }
    }
  }
</script>

<style>
  .theme--light h1 {
    font-weight: 300;
    color: #45474d;
    font-size: 1.8rem;
  }
  .theme--light.v-stepper {
    background-color: transparent;
  }
  .button-bar {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .theme--light.v-btn {
    text-transform: none;
    border-radius: 26px;
    padding-left: 26px;
    padding-right: 26px;
  }
  .theme--light.confirm {
    border: 1px solid lightgrey;
    padding: 30px 60px;
    text-align: center;
  }
  .confirm-msg {
    font-size: 1.6rem;
    color: grey;
    width: 480px;
    margin: 20px auto;
  }
  .theme--light.checkmark {
    color: #22a3ac;
    font-weight: bold;
    border: 2px solid #22a3ac;
    width: 60px;
    padding: 10px;
    border-radius: 30px !important;
  }
  .footnote {
    color: grey;
    font-size: .9rem;
  }
  .v-stepper, .v-stepper__header {
    box-shadow: none;
  }
  .v-stepper__content {
    padding: 0 25px;
  }
  .formContainer {
    display: flex;
    margin: 20px;
  }
  .formCol {
    flex: 1;
    margin: 20px;
  }
  .v-input {
    margin: 30px 0;
  }
</style>

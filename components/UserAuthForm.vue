<template>
  <v-form v-model="valid">
    <div @keydown.enter="submitForm(userInfo)">
      <v-text-field v-model="userInfo.name" 
                    label="Name" 
                    :rules="[required('name')]"
                    v-if="hasName" />

      <v-text-field v-model="userInfo.email" 
                    label="Email" 
                    :rules="[required('email'), emailFormat()]"/>

      <v-text-field v-model="userInfo.password"
                    label="Password"
                    :type="showPassword ? 'text' : 'password'" 
                    :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
                    @click:append="showPassword = !showPassword"
                    counter=true
                    :rules="[required('password'), minLength('password', 8)]"
                    />

      <v-btn @click="submitForm(userInfo)" :disabled="!valid">{{ buttonText }}</v-btn>
    </div>
  </v-form>
</template>

<script>
  import validations from "@/utils/validations";

  export default {
    data() {
      return {
        valid: false,
        showPassword: false,
        userInfo: {
          name: '',
          email: '',
          password: ''
        },
        ...validations
      }
    },
    props: {
      submitForm: {
        type: Function,
        required: true
      },
      buttonText: {
        type: String,
        required: true
      },
      hasName: Boolean
    }
  }
</script>

<style lang="scss" scoped>

</style>
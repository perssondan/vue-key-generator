<template>
    <n-space vertical style="align-self: center;">
      <n-input
        v-model:value="generatedPassword"
        type="textarea"
        placeholder="Password"
        readonly="true"
      />
      <n-checkbox v-model:checked="useLowerCaseCharacters">Use lower case characters</n-checkbox>
      <n-checkbox v-model:checked="useUpperCaseCharacters">Use upper case characters</n-checkbox>
      <n-checkbox v-model:checked="useNumbers">Use numbers</n-checkbox>
      <n-checkbox v-model:checked="useSpecialCharacters">Use special characters</n-checkbox>
      <n-checkbox v-model:checked="useLocaleCharacters">Use locale characters (å, ä, ö)</n-checkbox>
      <n-slider v-model:value="passwordLength" :max="25" :min="5" />
      <n-input-number v-model:value="passwordLength" :max="25" :min="5" />
      <n-button @click="generatePassword">Generate!</n-button>
    </n-space>
</template>

<script>
  import { ref } from "vue";
  import { NInput, NSpace, NCheckbox, NButton, NSlider, NInputNumber } from 'naive-ui'

  export default {
    name: 'KeyGen',
    components: {
        NInput,
        NSpace,
        NCheckbox,
        NButton,
        NSlider,
        NInputNumber
    },
    setup() {
      return {
        value: ref(null)
      };
    },
    data() {
        return {
            charactersLowerCase: ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n'],
            charactersUpperCase: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N'],
            numbers: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
            specialCharacters: ['-', '@', '!', '#', '$', '%', '^', '&', '*', '=', '+', '-', ',', '.', '<', '>'],
            generatedPassword: 'hejsan svejsan',
            passwordLength: 10,
            useLowerCaseCharacters: true,
            useUpperCaseCharacters: true,
            useNumbers: false,
            useSpecialCharacters: false
        }
    },
    methods: {
        generatePassword() {
            let newPassword = '';
            const passwordSource = this.getPasswordSources();

            for (let index = 0; index < this.passwordLength; index++) {
                newPassword = `${newPassword}${this.getRandomCharacter(passwordSource)}`
            }
            this.generatedPassword = newPassword;
        },
        getRandomCharacter(source) {
            const index = this.randomIntFromInterval(1, source.length - 1);
            console.log('index: ', index);
            return source[index];
        },
        randomIntFromInterval(min, max) { // min and max included 
            return Math.floor(Math.random() * (max - min + 1) + min)
        },
        getPasswordSources() {
            let passwordSource = [];
            if (this.useLowerCaseCharacters) {
                passwordSource = [...passwordSource, ...this.charactersLowerCase];
            }
            if (this.useUpperCaseCharacters) {
                passwordSource = [...passwordSource, ...this.charactersUpperCase];
            }
            console.log('passwordSource: ', passwordSource.length);
            if (this.useNumbers) {
                passwordSource = [...passwordSource, ...this.numbers];
            }
            console.log('passwordSource: ', passwordSource.length);
            if (this.useSpecialCharacters) {
                passwordSource = [...passwordSource, ...this.specialCharacters];
            }
            console.log('passwordSource: ', passwordSource.length);
            return passwordSource;
        }
    }
  }
</script>
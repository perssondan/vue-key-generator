<template>
    <n-space vertical>
      <n-input v-model:value="generatedPassword" type="text" placeholder="Basic Input" />
      <n-input
        v-model:value="generatedPassword"
        type="textarea"
        placeholder="Basic Textarea"
      />
      <n-checkbox v-model:checked="useCharacters">Use characters</n-checkbox>
      <n-checkbox v-model:checked="useNumbers">Use numbers</n-checkbox>
      <n-checkbox v-model:checked="useSpecialCharacters">Use special characters</n-checkbox>
      <n-button @click="generatePassword">Generate!</n-button>
    </n-space>
</template>

<script>
  import { ref } from "vue";
  import { NInput, NSpace, NCheckbox, NButton } from 'naive-ui'

  export default {
    name: 'KeyGen',
    components: {
        NInput,
        NSpace,
        NCheckbox,
        NButton
    },
    setup() {
      return {
        value: ref(null)
      };
    },
    data() {
        return {
            characters: ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n'],
            numbers: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
            specialCharacters: ['-', '@', '!', '#', '$', '%', '^', '&', '*', '=', '+', '-', ',', '.', '<', '>'],
            generatedPassword: 'hejsan svejsan',
            passwordLength: 10,
            useCharacters: true,
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
            if (this.useCharacters) {
                passwordSource = [...passwordSource, ...this.characters];
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
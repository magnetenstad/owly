<template>
  <h1>Welcome to Owly! 🦉</h1>
  <div class="col">
    <label for="name">I would like to learn about</label>
    <input id="name" type="text" v-model="subject" />
    <br />
    <label for="author-options">Questions should be</label>
    <RadioButtons
      id="author-options"
      name="author-options"
      :buttons="[
        { value: 'ai', label: 'generated by AI' },
        { value: 'user', label: 'written by me' },
      ]"
      @input="optionInput"
    ></RadioButtons>
    <br />
    <div>
      <button :disabled="submitDisabled" @click="submit">Submit</button>
    </div>
    <br />
    <span
      >Experimental:
      <router-link to="/bookshelf">browse bookshelf</router-link></span
    >
  </div>
</template>

<script lang="ts" setup>
import RadioButtons from '@/components/RadioButtons.vue'
import { RouterLink } from 'vue-router'
import { router } from '@/router'
import { ref, computed } from 'vue'

const subject = ref('')
const option = ref('')

const optionInput = (e: Event) => {
  option.value = (e.target as HTMLInputElement).value
}

const submitDisabled = computed(() => !option.value || !subject.value)

const submit = () => {
  if (option.value == 'ai') {
    router.push({ name: 'quiz', query: { subject: subject.value } })
    return
  }
  if (option.value == 'user') {
    router.push({ name: 'edit', query: { subject: subject.value } })
  }
}
</script>

<style scoped>
label {
  margin: 1em 0 1em;
}
</style>

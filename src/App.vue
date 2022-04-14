<template>
  <RDSInput @lookup-pi="convertPi" />
</template>

<script>
import RDSInput from './components/RDSInput.vue'

export default {
  name: 'App',
  components: {
    RDSInput
  },
  methods: {
    convertPi(piCode) {
      console.log(piCode)
    }
  }
}
</script>

<style>
body {
  font-family: 'Poppins', sans-serif; 
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  font-size: 1.5rem;
  /* background-color:#222222; */
}
</style>

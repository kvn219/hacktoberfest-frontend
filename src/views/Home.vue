<template>
  <div class="home">
    <AppCalculator></AppCalculator>
  </div>
</template>

<script>
// @ is an alias to /src
import AppCalculator from '@/components/AppCalculator.vue'

export default {
  name: 'home',
  components: {
    AppCalculator
  }
}
</script>

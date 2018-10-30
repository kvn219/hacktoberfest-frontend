<template>
  <div class="basic">
    <AppCalculator></AppCalculator>
  </div>
</template>

<script>
// @ is an alias to /src
import AppCalculator from '@/components/AppCalculator.vue'

export default {
  name: 'basic',
  components: {
    AppCalculator
  }
}
</script>

<template>
  <div class="basic">
    <AppPhoto></AppPhoto>
  </div>
</template>

<script>
// @ is an alias to /src
import AppPhoto from '@/components/AppPhoto.vue'

export default {
  name: 'basic',
  components: {
    AppPhoto
  }
}
</script>

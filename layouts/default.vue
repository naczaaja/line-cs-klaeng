<template>
  <v-app>
    <nuxt />
    <Dialog />
  </v-app>
</template>

<!-- เพิ่ม component -->
<script>
import Dialog from '~/components/Dialog.vue';
export default {
  components: {
    Dialog
  }
}
</script>

<style lang="scss">
.v-application {
  font-family: 'Prompt', sans-serif;
}

.v-toolbar__title {
  text-align: center;
  width: 100%;
  font-weight: bold;
}

.v-application .primary {
  background-color: #3c1361 !important;
  border-color: #3c1361 !important;
}

.text-primary {
  color: #3c1361;
}

.text-title {
  font-size: 20px;
  font-weight: bold;
}

.v-application .primary--text {
  color: #3c1361 !important;
  caret-color: #3c1361 !important;
}

.w-100 {
  width: 100%;
}
</style>

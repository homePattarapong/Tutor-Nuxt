<template>
  <v-app>
    <nuxt></nuxt>
    <Dialog />
  </v-app>
</template>
<script>
import Dialog from "~/components/Dialog";

export default {
  components: {
    Dialog
  }
}
</script>

<style lang="scss" >
.v-application {
  font-family: "Sarabun", sans-serif;
}
.v-toolbar__title {
  text-align: center;
  width: 100%;
  font-weight: bold;
}
.v-application .primary {
  background-color: #1a56be !important;
  border-color: #1a56be !important;
}
.text-primary {
  color: #1a56be;
}
.text-main{
  font-size: 20px;
}
.text-title {
  font-size: 20px;
  font-weight: bold;
}
.w-100 {
  width: 100%;
}
</style>

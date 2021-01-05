<template>
  <q-page>
    <Gallery category="nature" />
  </q-page>
</template>
<script lang="ts">
import { defineComponent, ref, reactive } from "@vue/composition-api";
import Gallery from "components/Gallery.vue"

export default defineComponent({
  name:"NaturePage",
  components: {Gallery},
})
</script>
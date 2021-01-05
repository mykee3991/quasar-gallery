<template>
  <q-page>
    <Gallery />
  </q-page>
</template>
<script lang="ts">
import { defineComponent, ref, reactive } from "@vue/composition-api";
import Gallery from "components/Gallery.vue"

export default defineComponent({
  name:"HomePage",
  components: {Gallery},
})
</script>
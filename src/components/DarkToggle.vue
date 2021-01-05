<template>
  <q-toggle v-model="isDark" color="dark" icon="tonality" @input="setDarkMode">
    <q-tooltip>
      {{isDark ? 'Disable Dark Mode' :'Enable Dark Mode'}}
    </q-tooltip>
  </q-toggle>
</template>
<script lang="ts">
import { defineComponent, ref } from "@vue/composition-api";
import { State, Method } from "components/models" 
export default defineComponent({
  name: "DarkToggleComponent",
  setup(_, context: any){
    const root: any = context.root
    const isDark = ref<boolean>(false)
    
    function setDarkMode () {
      root.$q.dark.set(isDark.value);
    }
    return {isDark, setDarkMode}
  }
})
</script>
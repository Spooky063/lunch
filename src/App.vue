<template>
  <List />
</template>

<script>
import { defineComponent } from 'vue'
import List from './components/List.vue'

const App = defineComponent({
  name: 'App',

  components: {
    List
  }
})

export default App;
</script>

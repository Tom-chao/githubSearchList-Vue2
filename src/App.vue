<template>
  <div class="container">
    <SearchComponents />
    <ListComponents />
  </div>
</template>
<script>
import SearchComponents from './components/Search.vue'
import ListComponents from './components/List.vue'

export default {
  name: 'App',
  components: {
    SearchComponents,
    ListComponents
  }
}
</script>
<style></style>

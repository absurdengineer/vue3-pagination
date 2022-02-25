<script>
import { defineComponent } from 'vue';
import Vue3Pagination from '@/vue3-pagination.vue';

export default defineComponent({
  name: 'ServeDev',
  components: {
    Vue3Pagination
  }
});
</script>

<template>
  <div id="app">
    <vue3-pagination />
  </div>
</template>

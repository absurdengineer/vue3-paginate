<script>
import { defineComponent } from 'vue';
import Vue3Paginate from '@/vue3-paginate.vue';

export default defineComponent({
  name: 'ServeDev',
  components: {
    Vue3Paginate
  }
});
</script>

<template>
  <div id="app">
    <vue3-paginate />
  </div>
</template>

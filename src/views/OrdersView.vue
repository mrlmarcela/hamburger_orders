<template>
  <div class="container-fluid p-5 mb-5">
    <p class="fs-2 fw-bold text-center mb-5">Manage orders</p>
    <div class="pt-3 mb-5">
      <Dashboard />
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Dashboard from '../components/Dashboard.vue';

@Options({
  components: {
    Dashboard,
  },
})

export default class OrdersView extends Vue {}
</script>
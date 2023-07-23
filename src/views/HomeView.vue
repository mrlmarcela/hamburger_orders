<template>
  <Banner />
  <div class="container pt-4">
    <p class="fs-2 fw-bold text-center">Assemble your burger</p>
    <BurgerForm />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Banner from '../components/Banner.vue';
import BurgerForm from '../components/BurgerForm.vue';

@Options({
  components: {
    Banner,
    BurgerForm,
  },
})
export default class HomeView extends Vue {}
</script>

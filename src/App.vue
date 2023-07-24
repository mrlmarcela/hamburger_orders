<template lang="en">
  <div class="d-flex flex-column h-100">
    <Navbar :logo="logo_src" :alt="app_name"/>
    <div class="flex-grow-1">
      <router-view/>
    </div>
    <Footer />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';

@Options({
  components: {
    Navbar,
    Footer,
  },
})
export default class App extends Vue {

  public logo_src: string;
  public app_name: string;

  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Make Your Burger",
    }
  }
}
</script>
<style>
html, body, #app {
  height: 100%;
}

.container{
  min-height: 250px;
}
</style>

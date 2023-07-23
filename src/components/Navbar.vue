<template>
    <div id="nav" class="bg-dark p-2 d-flex justify-content-end align-items-center fw-bold">
        <router-link class="ms-0 m-auto" to="/">
            <img style="width: 45px" :src="logo" :alt="alt">
        </router-link>
        <router-link to="/">Home</router-link>
        <router-link to="/orders">Orders</router-link>
    </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';

@Options({
  props: {
    logo: String,
    alt: String
  },
})

export default class Navbar extends Vue {

    public logo: string;
    public alt: string;

}
</script>

<style scoped>
    #nav a{
        transition: .3s;
        color: #FFF;
        text-decoration: none;
        padding: 5px 15px;
    }

    #nav a:hover{
        color: #FCBA03;
    }
</style>
<template>
    <div id="banner" class="pt-4 d-flex justify-content-start align-items-center">
        <p class="fs-1 fw-bold text-light p-5">Make Your Burger</p>
    </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class Banner extends Vue {}
</script>

<style scoped>
    #banner{
        background-image: url('./../../public/img/burger.jpg');
        background-position: center;
        background-size: 100%;
        min-height: 550px;
        background-repeat: no-repeat;
    }
</style>
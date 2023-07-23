<template>
    <div id="footer" class="bg-dark p-2 d-flex justify-content-center text-light w-100 p-4">
        <div>
            <p class="mb-3">Make Your Burger &copy; 2023</p>
            <div class="d-flex justify-content-center align-items-center">
                <img src="/img/linkedin.png" style="height: 20px;" alt="linkedin">
                <a href="https://www.linkedin.com/in/marcela--lima/" class="ps-2 text-light" style="text-decoration: none;" target="_blank">Marcela Lima</a>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component';

export default class Footer extends Vue {}
</script>
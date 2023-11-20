<script setup>
import { ref } from "vue";

const counter = ref(0);

</script>
<template>
    <div class="wrapper">
        <label>
            {{ counter }}
            <button type="button" @click="counter++">Click Me</button>
        </label>
    </div>
</template>
<style scoped>

.wrapper {
    padding: 2rem 1rem;
    border: 1px solid #999;
    overflow: hidden;
}

</style>
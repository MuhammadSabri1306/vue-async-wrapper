<script setup>
import { ref } from "vue";
import { useAsyncManualWrapper } from "../AsyncWrapper";
import axios from "axios";

const props = defineProps({
    isReject: { type: Boolean, default: false }
});

const baseURL = !props.isReject ? "https://randomuser.me/api" : "https://randomusers.me/api";
const http = axios.create({
    baseURL,
    timeout: 2000
});

const { resolveComponent, rejectComponent } = useAsyncManualWrapper();

const data = ref(null);
http.get("/")
    .then(response => {
        data.value = JSON.stringify(response.data);
        resolveComponent();
    })
    .catch(err => {
        console.error();
        rejectComponent();
    });

</script>
<template>
    <div class="wrapper">
        {{ data }}
    </div>
</template>
<style scoped>

.wrapper {
    padding: 2rem 1rem;
    border: 1px solid #999;
    overflow: hidden;
}

</style>
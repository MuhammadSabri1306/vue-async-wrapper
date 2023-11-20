<script setup>
import { ref, defineAsyncComponent, useAttrs } from "vue";

const emit = defineEmits(["resolve", "error"]);
const props = defineProps({
    loader: { type: Function, required: true },
});

const attrs = useAttrs();
const loadingState = ref("loading");

const AsyncComponent = defineAsyncComponent(async () => {
    try {

        const comp = await props.loader();
        loadingState.value = "resolve";
        return comp;

    } catch(err) {

        console.error(err);
        loadingState.value = "error";

    }
});
</script>
<template>
    <AsyncComponent v-show="loadingState == 'resolve'" v-bind="attrs" />
    <div v-if="loadingState == 'error'">
        <slot name="error"></slot>
    </div>
    <div v-else-if="loadingState == 'loading'">
        <slot name="loading"></slot>
    </div>
</template>
<script>
    export default { inheritAttrs: false };
</script>
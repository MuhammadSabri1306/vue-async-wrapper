<script setup>
import { ref, computed, defineAsyncComponent, useAttrs, provide, onMounted } from "vue";
import { asyncSetupInjectionKey } from "./index";

const emit = defineEmits(["resolve", "error"]);
const props = defineProps({
    loader: { type: Function, required: true },
});

const attrs = useAttrs();

const parentState = ref("loading");
const childState = ref("loading");
const loadingState = computed(() => {
    const pState = parentState.value;
    const cState = childState.value;
    
    if(pState == "loading")
        return "loading";
    if(pState == "resolve" && cState == "loading")
        return "loading";
    if(pState == "resolve" && cState == "resolve")
        return "resolve";
    return "error";
});

provide(asyncSetupInjectionKey, {
    childState: childState,
    setChildState: val => {
        if(["resolve", "error"].indexOf(val) < 0)
            return;
        childState.value = val;
    }
});

const AsyncComponent = defineAsyncComponent(async () => {
    try {

        const comp = await props.loader();
        parentState.value = "resolve";
        return comp;

    } catch(err) {

        console.error(err);
        parentState.value = "error";

    }
});
</script>
<template>
    <Suspense>
        <AsyncComponent v-show="loadingState == 'resolve'" v-bind="attrs" />
    </Suspense>
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
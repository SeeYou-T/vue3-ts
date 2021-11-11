<template >
    <div>{{ msg }}</div>
    <button @click="emitFn">加倍</button>
    <Suspense>
        <template #default>
            <AsyncComp />
        </template>
        <template v-slot:fallback>
            <h1>loading!!!!!!!!!!!!!!</h1>
        </template>
    </Suspense>
</template>
<script lang="ts">
import { defineComponent, defineAsyncComponent } from 'vue';
const AsyncComp = defineAsyncComponent(() => import("./suspense.vue"))
export default defineComponent({
    name: "Child",
    props: ["msg", "data",],
    components: { AsyncComp },
    setup(props, { attrs, slots, emit }) {
        console.log(props)
        console.log(attrs, slots, emit)
        const emitFn = (value: any) => {
            emit('click', value);
        };
        const emitFn2 = () => {
            emit('show');
        };
        return {
            emitFn,
            emitFn2
        }
    }
})
</script>
<style lang="">
    
</style>
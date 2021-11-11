<template >
    <div>suspense : {{ msg }}</div>
</template>
<script lang="ts">
export default {
    name: "AsyncComp",
    setup() {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve({
                    msg: 'abc'
                })
            }, 2000)
        })
    }
}
</script>
<style lang="">
    
</style>
<template>
    <div>
        <h2>Second component</h2>
        <h3>{{count}}</h3>
        <button @click="count++">Increment</button>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                count: 0
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>
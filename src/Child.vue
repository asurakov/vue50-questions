<template>
    <div class="user">
        {{user}}
    </div>
</template>

<script>
    export default {
        inject: ['user']
    }
</script>

<style scoped>
.user {
    display: flex;
}

</style>
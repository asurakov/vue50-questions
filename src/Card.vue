<template>
    <div class="card">
        <h2>
            <slot name="header"></slot>
        </h2>
        <div style="margin-top: 20px">
            <slot name="body"></slot>
        </div>
        <div style="margin-top: 15px; margin-left: auto;">
            <slot name="actions"></slot>
        </div>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>

</style>
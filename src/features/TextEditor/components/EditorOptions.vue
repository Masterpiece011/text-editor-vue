<template>
    <div class="options-wrapper">
        <slot></slot>
    </div>
</template>

<script>
export default {
    name: "editor-options"
}
</script>

<style scoped>
    .options-wrapper {
        display: flex;
    }
</style>
<template>
    <div class="item">
        <slot />
    </div>
</template>

<script>
export default {
    setup() {


        return {}
    }
}
</script>

<style lang="less" scoped>
.item {
    height: 5.125rem;
    border: 1px solid blue;
    margin: .25rem;
    background-color: rgba(13, 130, 255, .851);
}
</style>
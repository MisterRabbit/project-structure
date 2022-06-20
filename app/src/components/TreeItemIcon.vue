<script setup>
import { ref } from 'vue'

defineProps({
  type: {type: String, required: true}
})
</script>

<template>
    <div class="tree-item__icon">
        <img src="../assets/icon-folder.svg" v-if="type === 'folder'">
        <img src="../assets/icon-js.svg" v-else-if="type === 'js'">
        <img src="../assets/icon-scss.svg" v-else-if="type === 'scss'">
        <img src="../assets/icon-vue.svg" v-else>
    </div>
</template>

<style lang="scss" scoped>
    .tree-item__icon {
        display: flex;
        width: 18px;
        margin-right: 10px;
    }
</style>

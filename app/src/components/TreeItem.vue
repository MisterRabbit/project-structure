<script setup>
    import TreeItemIcon from './TreeItemIcon.vue'
    defineProps({
        itemData: { type: Object, required: true,}
    })
</script>

<template>
    <div class="tree-item">
        <div class="tree-item__data">
            <TreeItemIcon/>
            {{ itemData.title }}
        </div>
        <div class="tree-item__children" v-if="itemData.children">
            <TreeItem
                v-for="item in itemData.children"
                :key="item.title"
                :itemData="item"
            />

        </div>
    </div>
    <div class="tree-item">
    </div>
</template>

<style scoped>
</style>

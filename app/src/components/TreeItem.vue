<script setup>
    import TreeItemIcon from './TreeItemIcon.vue'
    defineProps({
        itemData: { type: Object, required: true,}
    })
    const emit = defineEmits(['changeActive'])


    const toggleActive = (data) => {
        emit('changeActive', data)
    }
</script>

<template>
    <div class="tree-item">
        <div class="tree-item__data">
            <div
                v-if="itemData.type === 'folder' && itemData.children && itemData.children.length"
                class="tree-item__arrow"
                @click="toggleActive(itemData)"
            >
                <img
                    src="../assets/icon-arrow.svg"
                    :class="{open: itemData.active}"
                >
            </div>
            <TreeItemIcon :type="itemData.type"/>

            {{ itemData.title }}
        </div>
        <div class="tree-item__children" v-if="itemData.children && itemData.active">
            <TreeItem
                v-for="item in itemData.children"
                :key="item.title"
                :itemData="item"
                @changeActive="toggleActive"
            />

        </div>
    </div>
    <div class="tree-item">
    </div>
</template>

<style lang="scss" scoped>
    .tree-item {
        &__data {
            display: flex;
            height: 35px;
            position: relative;
            align-items: center;
        }
        &__arrow {
            position: absolute;
            left: -13px;
            cursor: pointer;
            width: 15px;
            height: 100%;
            top: 7px;
            user-select: none;
            img {
                transition: all .2s;
                &.open {
                    transform: rotate(90deg);
                }
            }
        }
        &__children {
            margin-left: 18px;
        }
    }
</style>

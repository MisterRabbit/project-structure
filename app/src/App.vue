<script setup>
import TreeItem from './components/TreeItem.vue';
import { structureOne } from './mocks/structureOne';
import { structureTwo } from './mocks/structureTwo';
import {computed, ref} from 'vue';


const addUniqueId = (object) => {
    object.id = Math.random();

    const addForChildren = (object) => {
        object.id = Math.random();
        if (object.children && object.children.length) {
            object.children.forEach(item => addForChildren(item))
        }
    }

    addForChildren(object)
}

addUniqueId(structureOne)
addUniqueId(structureTwo)

const activeTab = ref('structureOne')

const treeOne = ref(structureOne)
const treeTwo = ref(structureTwo)

const activeTree = computed(() => activeTab.value === 'structureOne' ? treeOne.value : treeTwo.value )

const changeActive = (data) => {

    const tree = activeTab.value === 'structureOne' ? treeOne.value : treeTwo.value

    const findItem = (item) => {
        if (item.id === data.id) return item;

        if (item.children) {
            for (let child of item.children) {
                const result = findItem(child)
                if (result) return result
            }
        }

    }
    const result = findItem(tree)
    result.active = !result.active
}

</script>

<template>
    <h1>Подходы к <span>модульно-ориентированной</span> структуре frontend проектов</h1>
    <div class="header">
        <button
            class="button--accent"
            :class="{'active': activeTab === 'structureOne'}"
            @click="activeTab = 'structureOne'"
        >
            Вариант 1
        </button>
        <button
            class="button--accent"
            :class="{'active': activeTab === 'structureTwo'}"
            @click="activeTab = 'structureTwo'"
        >
            Вариант 2
        </button>
    </div>
    <div class="tree">
        <TreeItem :itemData="activeTree" @changeActive="changeActive"/>
    </div>
</template>

<style lang="scss">
    body {
        background-color: #0f172a;
        background-image: url("./assets/lights.png");
        background-position: center center;
        background-repeat: no-repeat;
        background-attachment: fixed;
        //background-size: cover;
    }
    #app {
      font-family: Avenir, Helvetica, Arial, sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      text-align: center;
      color: #2c3e50;
      margin-top: 60px;
    }
</style>

<style lang="scss" scoped>
    h1 {
        color: white;
        margin-bottom: 50px;
        span {
            color: #f472b6
        }
    }
    .header {
        display: flex;
        gap: 20px;
        justify-content: center;
    }
    .button--accent {
        background-color: transparent;
        color: white;
        padding: 10px 20px;
        border-radius: 8px;
        cursor: pointer;
        border: none;
        transition: all .2s;
        &.active {
            background-color: #0ea5e9;
        }
    }

    .tree {
        margin: 50px auto;
        max-width: 500px;
        color: gainsboro;
        text-align: left;
    }
</style>

<script setup>
import TreeItem from './components/TreeItem.vue';
import { structureOne } from './mocks/structureOne';
import { ref } from 'vue';

const activeTab = ref('structureOne')

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
        <TreeItem :itemData="structureOne"/>
    </div>
</template>

<style lang="scss">
body {
    background: #0f172a;
}
h1 {
    color: white;
    margin-bottom: 50px !important;
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
        background-color: #6366f1;
    }

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

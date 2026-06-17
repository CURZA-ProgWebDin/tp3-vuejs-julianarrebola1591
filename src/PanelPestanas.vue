<template>
    <div class="container">
        <div class="tabs-container">
            <div class="tabs-item" @click="handleTabClick(tabName.TODAS)" :class="{ 'tabs-item-active': activeTabName === tabName.TODAS}">
                Todas
            </div>
            <div class="tabs-item" @click="handleTabClick(tabName.ELECTRONICA)" :class="{ 'tabs-item-active': activeTabName === tabName.ELECTRONICA}">
                Electronica
            </div>
            <div class="tabs-item" @click="handleTabClick(tabName.PERIFERICOS)" :class="{ 'tabs-item-active': activeTabName === tabName.PERIFERICOS}">
                Perifericos
            </div>
        </div>
        <Component :is="currentTab"/>
    </div>
</template>

<script setup>
import { shallowRef  } from 'vue'
import TabTodos from './components/tabs/TabTodos.vue'
import TabElectronica from './components/tabs/TabElectronica.vue'
import TabPerifericos from './components/tabs/TabPerifericos.vue'

    let currentTab =  shallowRef(null)
    let activeTabName = null

    const tabName = {
        TODAS:'todas',
        ELECTRONICA: 'electronica',
        PERIFERICOS: 'perifericos'
    }

    const tabs = {
        [tabName.TODAS]: TabTodos,
        [tabName.ELECTRONICA]: TabElectronica,
        [tabName.PERIFERICOS]: TabPerifericos
    }

    function handleTabClick(tabName) {
        this.activeTabName = tabName
        this.currentTab = this.tabs[tabName]
    }
</script>

<style>

.container{
    display: flex;
    flex-direction: column;
}

.tabs-container {
    display: flex;
    justify-content: center;
}

.tabs-item{
    padding: 10px;
    font-size: 16px;
    border-radius: 10px 10px 0px 0px;
    cursor: pointer;
}

.tabs-item:hover {
    background-color: #8260e9;
    color: white;
}

.tabs-item-active{
    background-color: #8260e9;
    color: white;
    cursor: pointer;
}
</style>
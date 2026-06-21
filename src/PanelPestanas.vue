<!-- Con respecto a la pregunta realizada en el TP ¿En qué situación conviene usar KeepAlive y en cuál no?
Entiendo que es conveniente ustilizarlo cuando queremos reducir la cantidad de peticiones al servidor que se realizan.
Si en nuestra pagina tenemos que movernos rapidamente entre las mismas tabs o secciones de la pagina, es conveniente
guardar el componente en caché para agilizar las transiciones y evitar que se hagan peticiones inecesarias.
Creo que no lo usaria cuando tengo que mostrar información que se está actualizando constantemente, ya que podriamos
estar mostrando información obsoleta que está guardada en la caché, por otro lado tambien puedemos quedarnos sin memoria
en la caché, asi que tiene limitaciones en la cantidad de componentes que vamos a "mantener vivos".-->

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
        <keep-alive>
            <Component :is="currentTab"/>
        </keep-alive> 
    </div>
</template>

<script setup>
import { shallowRef  } from 'vue'
import TabTodos from './components/tabs/TabTodos.vue'
import TabElectronica from './components/tabs/TabElectronica.vue'
import TabPeriferico from './components/tabs/TabPeriferico.vue'

    let currentTab =  shallowRef(TabTodos)
    let activeTabName = 'todas'

    const tabName = {
        TODAS:'todas',
        ELECTRONICA: 'electronica',
        PERIFERICOS: 'perifericos'
    }

    const tabs = {
        [tabName.TODAS]: TabTodos,
        [tabName.ELECTRONICA]: TabElectronica,
        [tabName.PERIFERICOS]: TabPeriferico
    }

    function handleTabClick(tabName) {
        console.log(activeTabName)
        this.activeTabName = tabName
        this.currentTab = this.tabs[tabName]
        console.log(activeTabName)
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
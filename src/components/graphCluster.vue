<script setup>
    import graph from './graph.vue'
    import {ref} from 'vue'

    function getRandomInt(max) {
        return Math.floor(Math.random() * max);
    }

    let randomData = []
    for (let i = 0; i<11; ++i) {
        let mesures = []
        let nbMes = getRandomInt(15) + 5;
        for (let j = 0; j<nbMes; ++j) {
            mesures.push({id:j, content:getRandomInt(100)/10})
        }
        randomData.push({
            id:i,
            name:"machine "+i,
            unit:"volt",
            records:mesures
        })
    }

    const datas = ref(randomData)
</script>

<template>
    <div class="cluster">
        <graph v-for="item in datas"
            :graphData="item"
            :key="item.id">
        </graph>
    </div>
</template>

<style scoped>
    .cluster {
        margin-top: 20px;
        margin-bottom: 20px;
        display: flex;
        flex-wrap: wrap;
        flex-direction: row;
        justify-content: space-around;
    }
</style>
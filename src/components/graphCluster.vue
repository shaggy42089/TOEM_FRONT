<script setup>
    import curve from './curve.vue'
    import {ref} from 'vue'
    import {getMockData} from './curve/mockCurve.vue'

    let appData = getMockData()
    const datas = ref(appData.plots)
    const origins = ref(appData.dataSources)
</script>

<template>
    <div class="cluster">
        <curve v-for="item in datas"
            :graphData="item"
            :sources="origins"
            :key="item.id">
    </curve>
    </div>
</template>

<style scoped>
    .cluster {
        margin-top: 20px;
        margin-bottom: 20px;
        display: flex;
        flex-flow: row wrap;
        justify-content: start;
    }
</style>
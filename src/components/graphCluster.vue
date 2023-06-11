<script setup>
    import curve from './curve.vue'
    import {ref} from 'vue'
    import {getCurves} from './curve/mockCurve.vue'

    let curves = getCurves()
    const datas = ref(curves)
</script>

<template>
    <div class="cluster">
        <curve v-for="item in datas"
            :graphData="item"
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
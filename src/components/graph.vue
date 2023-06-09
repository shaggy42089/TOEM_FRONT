<script setup>
    const props = defineProps({
        graphData: Object
    })

    function getMax(arr) {
        let max = arr.records[0].content;
        arr.records.forEach(rec => {
            max = Math.max(max, rec.content)
        })
        return max;
    }    
</script>

<template>
    <div class="chart-wrapper">
        <div :class="'chart chart-'+graphData.id">
            <table class="charts-css line show-heading show-data-axes show-4-secondary-axes show-labels labels-align-center">
                <caption class="mx-3"> {{graphData.name}} </caption>
                <tbody>
                    <tr v-if="graphData !== undefined" v-for="item in graphData.records">
                        <td v-if="item.id === 0" :style="'--start: 0.0; --size: '+ item.content/getMax(graphData) +';'"><span class="data"></span></td>
                        <td v-else :style="'--start:'+(graphData.records[item.id-1].content)/getMax(graphData)+'; --size: '+ item.content/getMax(graphData) +';'"><span class="data"></span></td>
                    </tr>
                </tbody>
            </table>
            <div class="primary-axis">time</div>
            <div class="data-axis">Volts</div>
        </div>
    </div>
</template>

<style scoped>
    .chart-wrapper {
        resize: both;
        overflow: hidden;
        min-height: 200px;
        max-height: 80%;
        min-width: 300px;
        max-width: 60%;
        padding: 10px 30px 10px 20px;
        display: inline-block;
        flex-grow: 1;
        flex-shrink: 0;
        margin: 20px 10px 0px 10px;
        

        transition: position 1s ease;
        border-radius: 5px;
        -webkit-box-shadow: 6px 6px 19px -2px rgba(87,87,87,0.75); 
        box-shadow: 6px 6px 19px -2px rgba(87,87,87,0.75);
    }

    tr {
        margin: 0 !important;
    }
    

    .chart {
        display: grid;
        align-items: center;
        justify-items: center;
        grid-template-columns: 50px 1fr;
        grid-template-rows: 250px 50px;
        grid-template-areas:
            "data-axis chart"
            ".         primary-axis";
    }
    .chart > table {
        grid-area: chart;
    }
    .chart > .primary-axis {
       grid-area: primary-axis;
    }
    .chart > .data-axis {
        grid-area: data-axis;
        writing-mode: tb-rl;
        transform: rotateZ(180deg);
    }
</style>
<script setup>
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  PointElement,
  CategoryScale,
  LinearScale,
  Filler
} from 'chart.js';
import { Line } from 'vue-chartjs';
import { hostStatusToColor } from './core/utils.vue';
ChartJS.register(Filler, CategoryScale, LinearScale, LineElement, PointElement, Title, Tooltip, Legend)

const props = defineProps({
    graphData: Object,
    sources: Object
})    

</script>

<template>
    <div :id="'chart-'+graphData.id" :class="'chart position-relative border border-' + hostStatusToColor(graphData.dataRecord.source.status)">
        <slot name="modalButton"></slot>
        <span class="reset-button position-absolute top-0 start-0 p-1 pointer" :onclick="() => graphData.dataRecord.records = []">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-arrow-counterclockwise" viewBox="0 0 16 16">
                <path fill-rule="evenodd" d="M8 3a5 5 0 1 1-4.546 2.914.5.5 0 0 0-.908-.417A6 6 0 1 0 8 2v1z"/>
                <path d="M8 4.466V.534a.25.25 0 0 0-.41-.192L5.23 2.308a.25.25 0 0 0 0 .384l2.36 1.966A.25.25 0 0 0 8 4.466z"/>
            </svg>
        </span>
        <Line :data="{
            labels: graphData.dataRecord.records.map(el => el.time),
            datasets: [{
                label : graphData.title || graphData.name,
                backgroundColor: graphData.fillColor || '#faacac',
                borderColor: graphData.lineColor || '#f87979',
                data: graphData.dataRecord.records.map(el => el.val),
                borderWidth: 1,
                tension: 0.4,
                fill: 'start'
            }]
        }" :options="{
            animation: true,
            maintainAspectRatio: false,
            plugins: {
                legend: {
                    display: true
                },
                tooltip: {
                    enabled: true
                }
            },            
            scales: {
                y: {
                    min: Number(graphData.Ymin),
                    max: Number(graphData.Ymax),
                    title: {
                        text: (graphData.Yunit || ''),
                        display: true
                    },
                    ticks: {
                        callback: (value, index, ticks) => {
                            return '' + value;
                        }
                    }
                },
                x: {
                    min: Number(graphData.Xmin),
                    max: Number(graphData.Xmax),
                    title: {
                        text: (graphData.Xunit || ''),
                        display: true
                    },
                    ticks: {
                        callback: (value, index, ticks) => {
                            return '' + value;
                        }
                    }
                }
            }
        }"/>
    </div>
</template>

<style lang="scss" scoped>
    $window-padding: 4vw;
    $chart-paddingX: 10px;
    $chart-padding-top: 30px;
    $chart-padding-bottom: 20px;
    $chart-per-line: 4;
    $chart-offset: 5px;
    .chart {
        resize: both;
        overflow: hidden;
        min-height: calc(((100vw / $chart-per-line) - 2*$chart-paddingX - ($window-padding / $chart-per-line))*0.7);
        max-height: 80vh;
        min-width: calc((100vw / $chart-per-line) - ($window-padding / $chart-per-line) - 2*$chart-paddingX - $chart-offset);
        max-width: calc(100vw - $window-padding - $chart-offset);
        padding: $chart-paddingX $chart-padding-top $chart-paddingX $chart-padding-bottom;
        display: inline-block;
        flex-shrink: 1;
        margin: 20px 10px 0px 10px;
        

        transition: position 1s ease;
        border-radius: 5px;
        -webkit-box-shadow: 6px 6px 19px -2px rgba(87,87,87,0.75); 
        box-shadow: 6px 6px 19px -2px rgba(87,87,87,0.75);
    }
</style>
<script setup>
import modal from './plotModal.vue';
import {openModal} from './plotModal.vue';
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
import { hostStatuses } from './core/constants.vue';
ChartJS.register(Filler, CategoryScale, LinearScale, LineElement, PointElement, Title, Tooltip, Legend)

const props = defineProps({
    graphData: Object,
    sources: Object
})    

</script>

<script>
    export function hostStatusToColor(status) {
        switch(status) {
            case hostStatuses.RUNNING:
                return "border-success"
            case hostStatuses.OFFLINE:
                return "border-danger"
            case hostStatuses.IDLE:
                return "border-warning"
            case hostStatuses.STOPPED:
                return "border-dark"
            default:
                return "border-danger"
        }
    }
</script>

<template>
    <div :id="'chart-'+graphData.id" :class="'chart position-relative border ' + hostStatusToColor(graphData.dataRecord.source.status)">
        <span class="reset-button position-absolute top-0 end-0 p-1 pointer" :onclick="() => openModal(graphData.id)">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-gear-fill" viewBox="0 0 16 16">
                <path d="M9.405 1.05c-.413-1.4-2.397-1.4-2.81 0l-.1.34a1.464 1.464 0 0 1-2.105.872l-.31-.17c-1.283-.698-2.686.705-1.987 1.987l.169.311c.446.82.023 1.841-.872 2.105l-.34.1c-1.4.413-1.4 2.397 0 2.81l.34.1a1.464 1.464 0 0 1 .872 2.105l-.17.31c-.698 1.283.705 2.686 1.987 1.987l.311-.169a1.464 1.464 0 0 1 2.105.872l.1.34c.413 1.4 2.397 1.4 2.81 0l.1-.34a1.464 1.464 0 0 1 2.105-.872l.31.17c1.283.698 2.686-.705 1.987-1.987l-.169-.311a1.464 1.464 0 0 1 .872-2.105l.34-.1c1.4-.413 1.4-2.397 0-2.81l-.34-.1a1.464 1.464 0 0 1-.872-2.105l.17-.31c.698-1.283-.705-2.686-1.987-1.987l-.311.169a1.464 1.464 0 0 1-2.105-.872l-.1-.34zM8 10.93a2.929 2.929 0 1 1 0-5.86 2.929 2.929 0 0 1 0 5.858z"/>
            </svg>
        </span>
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
                            return '$' + value;
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
                            return '$' + value;
                        }
                    }
                }
            }
        }"/>
    </div>
    <modal
        :graphData="graphData"
        :sources="sources"
    ></modal>
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
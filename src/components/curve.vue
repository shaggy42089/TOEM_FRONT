<script setup>
import { onMounted } from 'vue';
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
ChartJS.register(Filler, CategoryScale, LinearScale, LineElement, PointElement, Title, Tooltip, Legend)

const props = defineProps({
    graphData: Object
})    

</script>

<template>
    <div :id="'chart-'+graphData.id" class="chart">
        <Line :data="{
            labels: graphData.records.map(el => el.time),
            datasets: [{
                label :'machine' + graphData.id,
                backgroundColor: '#faacac',
                borderColor: '#f87979',
                data: graphData.records.map(el => el.val),
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
                    beginAtZero: true,
                    title: {
                        text: (graphData.Yunit || ''),
                        display: true
                    },
                },
                x: {
                    beginAtZero: true,
                    title: {
                        text: (graphData.Xunit || ''),
                        display: true
                    },
                }
            }
        }"/>
    </div>
</template>

<style scoped>
    .chart {
        resize: both;
        overflow: hidden;
        min-height: calc((25vw - 10px - 10px - 1vw)*0.7);
        max-height: 80vh;
        min-width: calc(25vw - 1vw - 10px - 10px - 5px);
        max-width: 80vw;
        padding: 10px 30px 10px 20px;
        display: inline-block;
        flex-shrink: 1;
        margin: 20px 10px 0px 10px;
        

        transition: position 1s ease;
        border-radius: 5px;
        -webkit-box-shadow: 6px 6px 19px -2px rgba(87,87,87,0.75); 
        box-shadow: 6px 6px 19px -2px rgba(87,87,87,0.75);
    }
</style>
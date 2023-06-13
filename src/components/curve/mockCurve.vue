<script>    
    import {generate} from "random-words"
    import hostStatuses from "../core/constants.vue"

    function getRandomInt(max) {
        return Math.floor(Math.random() * max);
    }

    function getRandomColor() {
        let res = Math.floor(Math.random()*16777215).toString(16);
        return '#' + res;
    }

    export function getMockData() {
        let randomData = {}

        randomData.dataSources = [];

        for (let i = 0; i<10; ++i) {
            randomData.dataSources.push({
                id    : i,
                name  : generate(),
                host  : "localhost",
                status: getRandomInt(Object.values(hostStatuses).length)
            });
        }

        randomData.dataRecords = []
        
        for (let i = 0; i<12; ++i) {
            let mesures = []
            let nbMes = getRandomInt(15) + 5;

            for (let j = 0; j<nbMes; ++j) mesures.push({id:j, val:getRandomInt(100)/10, time:j/10})

            randomData.dataRecords.push({
                id: i,
                source:randomData.dataSources[getRandomInt(randomData.dataSources.length-1)],
                records: mesures
            })
        }

        randomData.plots = []

        for (let i = 0; i<5; ++i) {
            randomData.plots.push({
                id : i,
                dataRecord : randomData.dataRecords[getRandomInt(randomData.dataRecords.length-1)],
                title: "customName "+i,
                isModalVisible: false,
                lineColor: getRandomColor(),
                fillColor: getRandomColor(),
                Yunit: "volt",
                Xunit: "time",
                Xmin: 0,
                Xmax: 10,
                Ymin: 0,
                Ymax: 10,
            })
        }

        return randomData;
    }    
</script>

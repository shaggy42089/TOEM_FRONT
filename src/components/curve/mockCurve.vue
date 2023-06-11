<script>    
    function getRandomInt(max) {
        return Math.floor(Math.random() * max);
    }

    function getRandomColor() {
        let res = Math.floor(Math.random()*16777215).toString(16);
        return '#' + res;
    }

    export function getCurves() {
        let randomData = []
        
        for (let i = 0; i<12; ++i) {
            let mesures = []
            let nbMes = getRandomInt(15) + 5;
            for (let j = 0; j<nbMes; ++j) {
                mesures.push({id:j, val:getRandomInt(100)/10, time:j/10})
            }
            randomData.push({
                id: i,
                name:"machine "+i,
                title: "customName "+i,
                isModalVisible: false,
                lineColor: getRandomColor(),
                fillColor: getRandomColor(),
                Yunit: "volt",
                Xunit: "time",
                Xmin: 0,
                Xmax: 2,
                Ymin: 0,
                Ymax: 10,
                isRunning: getRandomInt(2)%2 === 1,
                records: mesures
            })
        }

        return randomData;
    }    
</script>

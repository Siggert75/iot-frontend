<script>
    import FusionCharts from 'fusioncharts';
    import Timeseries from 'fusioncharts/fusioncharts.timeseries';
    import SvelteFC, { fcRoot } from 'svelte-fusioncharts';
    import { onMount } from 'svelte';
    import { bigdata } from './data';

    fcRoot(FusionCharts, Timeseries);

    const getTemp = async () => {
        let res = await fetch('https://api.darkfiber.no/temp');
        let datan = await res.json();

        let ee = [];
        datan.forEach((item) => {
            ee.push([item.timestamp, item.value])
        });

        return ee;
    }

    let temps;

    onMount(() => {
        temps = getTemp();
    });

    //setInterval(updateTemp, 1000*60);

    let yolo = [
    {
        "name": "Time",
        "type": "date",
        "format": "%s"
    },
    {
      "name": "Temp",
      "type": "number"
    }
    ]

    let gg = []
    bigdata.forEach((item) => {
        gg.push([item.timestamp, item.value])
    })


    const getChartConfig = (data, schema) => {
        const fusionDataStore = new FusionCharts.DataStore()
        const fusionTable = fusionDataStore.createDataTable(data, schema);

        return {
        type: 'timeseries',
        width: '100%',
        height: 550,
        renderAt: 'chart-container',
        dataFormat: 'json',
        dataSource: {
            data: fusionTable,
            caption: {
                text: 'Temperature readings from PI'
            },
            yAxis: [
                {
                    plot: {
                        value: 'Temp',
                        type: 'line'
                    },
                    title: 'Temp'
                }
            ]
        }
        };
    };
    
</script>

<div id="chart-container">
    <SvelteFC {...getChartConfig(gg, yolo)}/>
</div>
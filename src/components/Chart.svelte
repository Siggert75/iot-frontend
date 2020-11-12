<script>
    import FusionCharts from 'fusioncharts';
    import Timeseries from 'fusioncharts/fusioncharts.timeseries';
    import SvelteFC, { fcRoot } from 'svelte-fusioncharts';
    import yolo from './data';

    fcRoot(FusionCharts, Timeseries);

    let schema1 = [{
    "name": "Time",
    "type": "date",
    "format": "%-m/%-d/%Y"
}, {
    "name": "Sales",
    "type": "number"
}]

    const getChartConfig = ([data, schema]) => {
        const fusionDataStore = new FusionCharts.DataStore(),
        fusionTable = fusionDataStore.createDataTable(data, schema);

        return {
        type: 'timeseries',
        width: '100%',
        height: 450,
        renderAt: 'chart-container',
        dataSource: {
            data: fusionTable,
            caption: {
            text: 'Sales Analysis'
            },
            subcaption: {
            text: 'Grocery'
            },
            yAxis: [
            {
                plot: {
                value: 'Grocery Sales Value',
                type: 'line'
                },
                format: {
                prefix: '$'
                },
                title: 'Sale Value'
            }
            ]
        }
        };
    };
    
</script>

<div id="chart-container">
    <SvelteFC {...getChartConfig([yolo, schema1])}/>
</div>
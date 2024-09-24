<template>
    <div class="line-charts"></div>
</template>

<script>
import * as echarts from "echarts";

export default {
    data() {
        return {

        }
    },
    methods: {
        initChart() {
            let myChart = echarts.init(document.querySelector('.line-charts'))

            const option = {
                toolbox: {
                    feature: {
                        // dataView: { show: true, readOnly: false },
                        // magicType: { show: true, type: ['line', 'bar'] },
                        // restore: { show: true },
                        saveAsImage: { show: true }
                    }
                },
                legend: {
                    data: ['Evaporation', 'Precipitation', 'Temperature'],
                    itemWidth: 10,
                    itemHeight: 3,
                    icon: 'rect',
                },
                xAxis: {
                    type: 'category',
                    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
                },
                yAxis: [
                    {
                        type: 'value',
                        name: 'Precipitation',
                        min: 0,
                        max: 250,
                        interval: 50,
                        axisLabel: {
                            formatter: '{value} ml'
                        }
                    },
                    {
                        type: 'value',
                        name: 'Temperature',
                        min: 0,
                        max: 25,
                        interval: 5,
                        axisLabel: {
                            formatter: '{value} °C'
                        }
                    }
                ],
                series: [
                    {
                        name: 'Precipitation',
                        type: 'line',
                        tooltip: {
                            valueFormatter: function (value) {
                                return value + ' ml';
                            }
                        },
                        data: [
                            2.6, 5.9, 9.0, 26.4, 28.7, 70.7, 175.6, 182.2, 48.7, 18.8, 6.0, 2.3
                        ]
                    },
                    {
                        name: 'Temperature',
                        type: 'line',
                        yAxisIndex: 1,
                        tooltip: {
                            valueFormatter: function (value) {
                                return value + ' °C';
                            }
                        },
                        data: [2.0, 2.2, 3.3, 4.5, 6.3, 10.2, 20.3, 23.4, 23.0, 16.5, 12.0, 6.2]
                    }

                ]
            };
            myChart.setOption(option)
            window.addEventListener('resize', () => {
                myChart.resize()
            })

        }
    },
    mounted() {
        this.initChart()
    }
}
</script>
<style lang="scss" scoped>
.line-charts {
    height: 400px;
}
</style>
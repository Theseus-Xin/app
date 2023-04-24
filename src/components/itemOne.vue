<template>
    <div>
        <h2>图表1</h2>
        <div id="chartA" class="chart">
            容纳后期的图表
        </div>
    </div>
</template>

<script>
import { inject, onMounted, reactive } from 'vue';

export default {
    setup() {
        const $echarts = inject("echarts")
        const $http = inject("axios")
        async function getState() {
            data = await $http({ url: "one/data" })
            data = data.data.data
        }
        let data = reactive({})
        let xData = reactive({})
        let yData = reactive({})
        function setData() {
            xData = data.map(v => v.title)
            yData = data.map(v => v.num)
        }
        onMounted(() => {
            const myChart = $echarts.init(document.getElementById("chartA"))
            getState().then(() => {
                setData()
                myChart.setOption({
                    grid: {
                        top: "3%",
                        left:"1%",
                        right:"6%",
                        bottom:"3%",
                        containLabel:true
                    },
                    xAxis: {
                        type: "value",
                        axisLine: {
                            lineStyle: {
                                color: "#fff"
                            }
                        }
                    },
                    yAxis: {
                        type: "category",
                        data: xData,
                        axisLine: {
                            lineStyle: {
                                color: "#fff"
                            }
                        }
                    },
                    series: [
                        {
                            type: "bar",
                            data: yData,
                            itemStyle: {
                                normal: {
                                    barBorderRadius: [0, 20, 20, 0],
                                    color: new $echarts.graphic.LinearGradient(0, 0, 1, 0, [
                                        {
                                            offset: 0,
                                            color: "#005eaa"
                                        },
                                        {
                                            offset: 0.5,
                                            color: "#339ca8"
                                        },
                                        {
                                            offset: 1,
                                            color: "#cda819"
                                        },
                                    ])
                                }
                            }
                        }
                    ]
                })
                window.onresize = function () {
                    myChart.resize()
                }
            })
        })
        return {
            getState, setData,
            data, xData, yData,
        }
    }
}
</script>

<style lang="less" scoped>
h2 {
    height: 0.6rem;
    color: #fff;
    line-height: .6rem;
    text-align: center;
    font-size: .25rem;
}

.chart {
    height: 4.5rem;
}
</style>
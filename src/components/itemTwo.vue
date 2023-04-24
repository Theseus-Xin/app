<template>
    <div>
        <h2>图表2</h2>
        <div class="chart" id="chartB">
            容纳后期的图表
        </div>
    </div>
</template>

<script>
import { inject, onMounted, reactive } from "vue";
export default {
    setup() {
        const $echarts = inject("echarts")
        const $http = inject("axios")
        let data = reactive({})

        async function getState() {
            data = await $http({ url: "two/data" })
            data = data.data.data
        }

        onMounted(() => {
            getState().then(() => {
                let myChart = $echarts.init(document.getElementById("chartB"))
                myChart.setOption({
                    tooltip: {
                        trigger: "axis",
                        axisPointer: {
                            type: "cross",
                            label: {
                                backgroundColor: "#e6b600"
                            }
                        }
                    },
                    legend: {
                        data: ["服饰", "数码", "家电", "家居", "日化"]
                    },
                    grid: {
                        left: "1%",
                        right: "4%",
                        bottom: "3%",
                        containLabel: true
                    },
                    xAxis: [{
                        type: "category",
                        boundaryGap: false,
                        data: data.day
                    }],
                    yAxis: [{
                        type: "value",
                    }],
                    series: [
                        {
                            name: "服饰",
                            type: "line",
                            data: data.num.Chemicals,
                            stack: "Total", // 数据堆叠
                            smooth: true, // 折线图平滑效果，变成曲线图
                            showSymbol: false, // 隐藏所有数据点
                            areaStyle: { // 设置填充区域的样式
                                opacity: 0.8,
                                color: new $echarts.graphic.LinearGradient(0, 0, 0, 1, [
                                    {
                                        offset: 0,
                                        color: "rgb(128,255,165)"
                                    },
                                    {
                                        offset: 1,
                                        color: "rgb(1,191,236)"
                                    }
                                ])
                            },
                            lineStyle: {
                                width: 0
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },
                        {
                            name: "数码",
                            type: "line",
                            data: data.num.Clothes,
                            stack: "Total",
                            smooth: true,
                            showSymbol: false,
                            areaStyle: { // 设置填充区域的样式
                                opacity: 0.8,
                                color: new $echarts.graphic.LinearGradient(0, 0, 0, 1, [
                                    {
                                        offset: 0,
                                        color: "rgb(0,221,255)"
                                    },
                                    {
                                        offset: 1,
                                        color: "rgb(77,119,255)"
                                    }
                                ])
                            },
                            lineStyle: {
                                width: 0
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },
                        {
                            name: "家电",
                            type: "line",
                            data: data.num.Electrical,
                            stack: "Total",
                            smooth: true,
                            showSymbol: false,
                            areaStyle: { // 设置填充区域的样式
                                opacity: 0.8,
                                color: new $echarts.graphic.LinearGradient(0, 0, 0, 1, [
                                    {
                                        offset: 0,
                                        color: "rgb(55,162,255)"
                                    },
                                    {
                                        offset: 1,
                                        color: "rgb(116,21,219)"
                                    }
                                ])
                            },
                            lineStyle: {
                                width: 0
                            },
                            emphasis: {
                                focus: "series"
                            }

                        },
                        {
                            name: "家居",
                            type: "line",
                            data: data.num.digit,
                            stack: "Total",
                            smooth: true,
                            showSymbol: false,
                            areaStyle: { // 设置填充区域的样式
                                opacity: 0.8,
                                color: new $echarts.graphic.LinearGradient(0, 0, 0, 1, [
                                    {
                                        offset: 0,
                                        color: "rgb(255,0,135)"
                                    },
                                    {
                                        offset: 1,
                                        color: "rgb(135,21,157)"
                                    }
                                ])
                            },
                            lineStyle: {
                                width: 0
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },
                        {
                            name: "日化",
                            type: "line",
                            data: data.num.gear,
                            stack: "Total",
                            smooth: true,
                            showSymbol: false,
                            areaStyle: { // 设置填充区域的样式
                                opacity: 0.8,
                                color: new $echarts.graphic.LinearGradient(0, 0, 0, 1, [
                                    {
                                        offset: 0,
                                        color: "rgb(255,191,0)"
                                    },
                                    {
                                        offset: 1,
                                        color: "rgb(224,62,76)"
                                    }
                                ])
                            },
                            lineStyle: {
                                width: 0
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },
                    ]
                })
            })
        })

        return {
            data,
            getState
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
    // background-color: gray;
}
</style>
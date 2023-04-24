<template>
    <div>
        <h2>图表4</h2>
        <div class="chart" id="chartD">
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
                let myChart = $echarts.init(document.getElementById("chartD"))
                myChart.setOption({
                    xAxis: [{
                        axisLine: {
                            lineStyle: {
                                color: "#fff"
                            }
                        },
                        type: "category",
                        data: data.day
                    }],
                    yAxis: [{
                        axisLine: {
                            lineStyle: {
                                color: "#fff"
                            }
                        },
                        type: "value",
                    }],
                    tooltip: {
                        trigger: "axis",
                        axisPointer: {
                            type: "shadow"
                        }
                    },
                    legend: {},
                    grid: {
                        left: "3%",
                        right: "4%",
                        bottom: "3%",
                        containLabel: true
                    },
                    series: [
                        {
                            name: "服饰",
                            type: "bar",
                            data: data.num.Chemicals,
                            stack: "total", // 数据堆叠
                            label: {
                                show: true
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },
                        {
                            name: "数码",
                            type: "bar",
                            data: data.num.Clothes,
                            stack: "total", // 数据堆叠
                            label: {
                                show: true
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },
                        {
                            name: "家电",
                            type: "bar",
                            data: data.num.Electrical,
                            stack: "total", // 数据堆叠
                            label: {
                                show: true
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },
                        {
                            name: "家居",
                            type: "bar",
                            data: data.num.digit,
                            stack: "total", // 数据堆叠
                            label: {
                                show: true
                            },
                            emphasis: {
                                focus: "series"
                            }
                        },
                        {
                            name: "日化",
                            type: "bar",
                            data: data.num.gear,
                            stack: "total", // 数据堆叠
                            label: {
                                show: true
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
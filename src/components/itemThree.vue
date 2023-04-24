<template>
    <div>
        <h2>图表3</h2>
        <div class="chart" id="chartC">
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
            data = await $http({ url: "three/data" })
            data = data.data.data
            console.log(data);
        }

        onMounted(() => {
            getState().then(() => {
                let myChart = $echarts.init(document.getElementById("chartC"))
                myChart.setOption({
                    legend: { // 设置图例
                        top: "bottom",
                    },
                    series: [
                        {
                            name: "Nightingale Chart",
                            type: "pie", // 饼图
                            radius: [10, 100], // 饼图的半径数组的第一项是内半径，第二项是外半径
                            center: ["50%", "45%"], // 饼图的中心坐标，数组的第一项是横坐标，第二项是纵坐标
                            roseType: "area", // 设置成玫瑰图
                            itemStyle: {
                                borderRadius: 10, // 用于指定饼图扇形区域的内外半径
                            },
                            data,
                        }
                    ],
                    // // 设置饼状图的颜色
                    color: ["#c12e34", "#e6b600", "#0098d9", "#2b821d", "#005eaa", "#339ca8"],
                    // 提示框，鼠标悬停交互时的信息提示
                    tooltip: {
                        show: true,
                        borderRadius: 10,
                    }
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
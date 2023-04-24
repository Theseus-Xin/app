<template>
    <div class="map" id="map"> </div>
</template>

<script>
import { onMounted, reactive, inject } from "vue";
export default {
    setup() {
        let data = reactive({})
        const $echarts = inject("echarts")
        const $http = inject("axios")
        async function getState() {
            data = await $http({ url: "map/data" })
            data = data.data.data
        }
        onMounted(() => {
            getState().then(() => {
                $echarts.registerMap("china", data)
                const myChart = $echarts.init(document.getElementById("map"))
                myChart.setOption({
                    title: {
                        text: "城市销售量",
                        left: "45%",
                        textStyle: {
                            color: "#fff",
                            fontSize: 20,
                            textShadowBlur: 10,
                            textShadowCOlor: "#33ffff"
                        }
                    },
                    geo: {
                        map: "china",
                        itemStyle: {
                            areaColor: "#00ffff", // 地图区域颜色，
                            shadowColor: "rgba(230,130,70,.5)", // 图形描边颜色
                            shadowBlur: 30, // 图形阴影的模糊大小
                            emphasis: { // 高亮状态下的多边形标签样式
                                focus: "self" // 高亮图形时，是否淡出其它数据的图形已达到聚焦的效果，self只聚焦（不淡出）当前高亮的数据的图形
                            }
                        },
                    },
                    series: [
                        {
                            type: "scatter", // 类型散点图
                            itemStyle: {
                                color: "red",  // 散点图颜色
                            },
                            name: "所在城市销售额",
                            coordinateSystem: "geo", // 该系列使用的坐标系，geo使用地理坐标系
                            data: [
                                { name: "北京", value: [116.46, 39.92, 4367] },
                                { name: "上海", value: [121.48, 31.22, 8675] },
                                { name: "深圳", value: [114.07, 22.62, 2461] },
                                { name: "广州", value: [113.23, 23.16, 187] },
                                { name: "西安", value: [108.45, 34, 3421] },
                            ],

                        }
                    ],
                    tooltip: {
                        trigger: "item", // 提示框组件
                    },
                    visualMap: { // 视觉映射组件，地图左下角的选择器
                        type: "continuous", //连续型
                        min: 100, // 值域最小值
                        max: 5000, // 值域最大值
                        calculable: true, // 是否启用滑动空间
                        inRange: {
                            color: ["#50a3ba", "#eac736", "#d94e5d"] // 指定数值从低到高的颜色变化
                        },
                        texStyle: {
                            color: "#fff" //  值域控件的文本颜色
                        }
                    }
                })
            })
        })
        return {
            data
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

.map {
    width: 100%;
    height: 100%;

}
</style>
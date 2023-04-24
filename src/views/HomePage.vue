<template>
  <div class="home">
    <header>
      <h1>VUE-大数据可视化</h1>
    </header>
    <!-- 容器 -->
    <section class="container">
      <section class="itemLeft">
        <ItemPage>
          <ItemOne></ItemOne>
        </ItemPage>
        <ItemPage>
          <ItemTwo></ItemTwo>
        </ItemPage>
      </section>
      <section class="itemCenter">
        <MapPage></MapPage>
      </section>
      <section class="itemRight">
        <ItemPage>
          <ItemThree></ItemThree>
        </ItemPage>
        <ItemPage>
          <ItemFour></ItemFour>
        </ItemPage>
      </section>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
import ItemPage from '@/components/itemPage.vue';
import ItemOne from '@/components/itemOne.vue';
import ItemTwo from '@/components/itemTwo.vue';
import ItemThree from '@/components/itemThree.vue';
import ItemFour from '@/components/itemFour.vue';
import MapPage from '@/components/mapPage.vue';
import { inject } from "vue";
export default {
  name: 'HomeView',
  components: {
    ItemPage,
    ItemOne,
    ItemTwo,
    ItemThree,
    ItemFour,
    MapPage
  },
  setup() {
    let $echarts = inject("echarts")
    let $axios = inject("axios")
    console.log($echarts, $axios);
  }
}
</script>
<style lang="less">
header {
  height: 1rem;
  width: 100%;
  background-color: rgba(0, 0, 255, .2);

  h1 {
    font-size: .375rem;
    color: #fff;
    text-align: center;
    line-height: 1rem;
  }
}

.container {
  min-width: 1200px;
  max-width: 2048px;
  margin: 0 auto;
  padding: .125rem .125rem 0;
  display: flex;

  .itemLeft,
  .itemRight {
    flex: 3;
  }

  .itemCenter {
    flex: 5;
  }
}
</style>

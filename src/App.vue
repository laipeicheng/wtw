<template>
  <el-container :style="containerStyle">
    <el-main class="elmain">
      <bm-map
        class="bmview"
        ak="hnOd6GOCv4oVqEdFbaYgb0fCplQG4FkQ"
        :center="{lat: 23.503845,lng: 111.322852}"
        :zoom="17"
        :scroll-wheel-zoom="true"
        :map-click="false"
        :double-click-zoom="false"
        @ready="handler"
        @click="bmClick"
      >
        <bm-navigation anchor="BMAP_ANCHOR_TOP_RIGHT"/>
        <bm-control style="width: 100%">
            <div class="head">
                <div class="search">
                  <el-input v-model="input" style="width: 70%"/>
                  <el-button class="el-button--primary">搜索</el-button>
                </div>
            </div>
        </bm-control>
        <bm-marker
          :position="{lat: 23.503845,lng: 111.322852}"
          :dragging="true"
        >
        </bm-marker>
      </bm-map>
    </el-main>
  </el-container>
</template>
<script>
import ElContainer from 'element-ui/packages/container/src/main'
import ElHeader from 'element-ui/packages/header/src/main'
import ElMain from 'element-ui/packages/main/src/main'
import ElMenu from 'element-ui/packages/menu/src/menu'
import ElInput from 'element-ui/packages/input/src/input'
import ElButton from 'element-ui/packages/button/src/button'
import BmMap from 'vue-baidu-map/components/map/Map'
import BmNavigation from 'vue-baidu-map/components/controls/Navigation'
import BmMarker from 'vue-baidu-map/components/overlays/Marker'
import BmLabel from 'vue-baidu-map/components/overlays/Label'
import BmControl from 'vue-baidu-map/components/controls/Control'

export default {
  name: 'App',
  components: {
    BmMap,
    BmNavigation,
    BmMarker,
    BmLabel,
    BmControl,
    ElContainer,
    ElHeader,
    ElMain,
    ElMenu,
    ElInput,
    ElButton
  },
  data () {
    return {
      containerStyle: {
        height: (document.documentElement.clientHeight - 1) + 'px'
      },
      input: '',
      BMap: {}
    }
  },
  methods: {
    handler ({BMap, map}) {
      console.log(BMap, map)
      const that = this
      that.BMap = BMap
    },
    bmClick (e) {
      console.log(e.target.getCenterPoint())
    }
  },
  mounted () {
    const that = this
    window.onresize = function () {
      that.containerStyle.height = (document.documentElement.clientHeight - 1) + 'px'
    }
  }
}

</script>

<style>

  .elmain {
    height: 100%;
    padding: 0px;
  }

  .bmview {
    width: 100%;
    height: 100%;
  }

  .head {
    width: 100%;
    height: 60px;
    line-height: 60px
  }

  .search {
    width: 80%;
    height: 100%;
    margin-left: 5%;
    text-align: center;
    line-height: 60px
  }

  @media screen and (min-width: 700px) {
    .search {
      width: 85%;
      margin-left: 10%;
    }
  }
</style>

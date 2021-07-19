<template>
  <div id="app">
    <!-- Header -->
    <app-header :poiInfo="poiInfo"></app-header>
    <!-- Nav -->
    <app-nav :commentNum="commentNum"> </app-nav>
    <!-- Container -->
    <keep-alive>
    <router-view></router-view>
    </keep-alive>
  </div>
</template>
<script>
import Header from './components/header/Header.vue';
import Nav from './components/nav/Nav.vue';
export default {
  name: 'App',
  data: function() {
    return {
      poiInfo:{},
      commentNum:0
    }
  },
  components: {
    "app-header":Header,
    "app-nav":Nav
  },
  // header获取数据
  // axios
  
  // fetch
  created: function() {
    fetch("/api/goods")
      .then(res => {
        return res.json();
      })
      .then(response => {
        // console.log(response);
        if(response.code == 0){
          this.poiInfo = response.data.poi_info;
          // console.log(this.poiInfo);
        };
      })
    fetch("/api/ratings")
      .then(res => {
        return res.json();
      })
      .then(response => {
        if(response.code == 0){
          this.commentNum = response.data.comment_num;
        };
      })
  },
}
</script>

<style>
    /* 全局引入从图标 */
    @import url(./common/css/icon.css);
</style>

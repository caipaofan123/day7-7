<template>
  <div>
    <MyHeaderVue title="你的tabbar" background="gold"></MyHeaderVue>
    <div style="margin-top: 45px">
      <component :is="componentN"></component>
    </div>
    <MyTabBarVue :list="list" @change="change"></MyTabBarVue>
  </div>
</template>

<script>
import MyHeaderVue from './components/MyHeader.vue';
import MyTabBarVue from './components/MyTabBar.vue';
import MyGoodsList from './views/MyGoodsList.vue';
import MyGoodsSearch from './views/MyUserInfo.vue'
import MyUserInfo from './views/MyGoodsSearch.vue';
export default {
  name: 'New7Tabbar',

  data() {
    return {
      componentN: 'MyGoodsList',
      list: [
        {
          iconText: 'icon-shangpinliebiao',
          text: '商品列表',
          componentName: 'MyGoodsList',
        },
        {
          iconText: 'icon-sousuo',
          text: '商品搜索',
          componentName: 'MyGoodsSearch',
        },
        {
          iconText: 'icon-user',
          text: '我的信息',
          componentName: 'MyUserInfo',
        },
      ],
    };
  },
  components: {
    MyHeaderVue,
    MyTabBarVue,
    MyGoodsList,
    MyGoodsSearch,
    MyUserInfo,
  },
  mounted() {},

  methods: {
    change(val){
        this.componentN=val
    }
  },
};
</script>

<style lang="scss" scoped></style>

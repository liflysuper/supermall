<template>
  <div id="home" class="wrapper">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <scroll class="content">
      <home-swiper :banners="banners"></home-swiper>
      <recommend-view :recommends="recommends"></recommend-view>
      <feature-view></feature-view>
      <tab-control class="tab-control" :titles="['流行','新款','精选']"
      @tabClick="tabClick"></tab-control>
      <good-list :goods="showGoods"></good-list>
    </scroll>
    <ul>
      <li>临时列表1</li>
      <li>临时列表2</li>
      <li>临时列表3</li>
      <li>临时列表4</li>
      <li>临时列表5</li>
      <li>临时列表6</li>
      <li>临时列表7</li>
      <li>临时列表8</li>
      <li>临时列表9</li>
      <li>临时列表10</li>
      <li>临时列表11</li>
      <li>临时列表12</li>
      <li>临时列表13</li>
      <li>临时列表14</li>
      <li>临时列表15</li>
      <li>临时列表16</li>
      <li>临时列表17</li>
      <li>临时列表18</li>
      <li>临时列表19</li>
      <li>临时列表20</li>
      <li>临时列表21</li>
      <li>临时列表22</li>
      <li>临时列表23</li>
      <li>临时列表24</li>
      <li>临时列表25</li>
      <li>临时列表26</li>
      <li>临时列表27</li>
      <li>临时列表28</li>
      <li>临时列表29</li>
      <li>临时列表30</li>
      <li>临时列表31</li>
      <li>临时列表32</li>
      <li>临时列表33</li>
      <li>临时列表34</li>
      <li>临时列表35</li>
      <li>临时列表36</li>
      <li>临时列表37</li>
      <li>临时列表38</li>
      <li>临时列表39</li>
      <li>临时列表40</li>
      <li>临时列表41</li>
      <li>临时列表42</li>
      <li>临时列表43</li>
      <li>临时列表44</li>
      <li>临时列表45</li>
      <li>临时列表46</li>
      <li>临时列表47</li>
      <li>临时列表48</li>
      <li>临时列表49</li>
      <li>临时列表50</li>
      <li>临时列表51</li>
      <li>临时列表52</li>
      <li>临时列表53</li>
      <li>临时列表54</li>
      <li>临时列表55</li>
      <li>临时列表56</li>
      <li>临时列表57</li>
      <li>临时列表58</li>
      <li>临时列表59</li>
      <li>临时列表60</li>
      <li>临时列表61</li>
      <li>临时列表62</li>
      <li>临时列表63</li>
      <li>临时列表64</li>
      <li>临时列表65</li>
      <li>临时列表66</li>
      <li>临时列表67</li>
      <li>临时列表68</li>
      <li>临时列表69</li>
      <li>临时列表70</li>
      <li>临时列表71</li>
      <li>临时列表72</li>
      <li>临时列表73</li>
      <li>临时列表74</li>
      <li>临时列表75</li>
      <li>临时列表76</li>
      <li>临时列表77</li>
      <li>临时列表78</li>
      <li>临时列表79</li>
      <li>临时列表80</li>
      <li>临时列表81</li>
      <li>临时列表82</li>
      <li>临时列表83</li>
      <li>临时列表84</li>
      <li>临时列表85</li>
      <li>临时列表86</li>
      <li>临时列表87</li>
      <li>临时列表88</li>
      <li>临时列表89</li>
      <li>临时列表90</li>
      <li>临时列表91</li>
      <li>临时列表92</li>
      <li>临时列表93</li>
      <li>临时列表94</li>
      <li>临时列表95</li>
      <li>临时列表96</li>
      <li>临时列表97</li>
      <li>临时列表98</li>
      <li>临时列表99</li>
      <li>临时列表100</li>
    </ul>
  </div>
</template>

<script>
import HomeSwiper from "./childComps/HomeSwiper";
import RecommendView from "./childComps/RecommendView";
import FeatureView from "./childComps/FeatureView";

import NavBar from "components/common/navbar/NavBar";
import TabControl from "components/content/tabControl/TabControl";
import GoodList from 'components/content/goods/GoodsList'
import Scroll from 'components/common/scroll/Scroll'

import { getHomeMultidata, getHomeGoods } from "network/home";


export default {
  name: "Home",
  components: {
    HomeSwiper,
    RecommendView,
    FeatureView,
    NavBar,
    TabControl,
    GoodList,
    Scroll
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: []},
        new: { page: 0, list: []},
        sell: { page: 0, list: []},
      },
      currentType: 'pop'
    }
  },
  computed:{
     showGoods(){
       return this.goods[this.currentType].list
     }
  },
  created() {
    //  1.请求多个数据
    this.getHomeMultidata()

    // 2.请求商品数据
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
  },
  methods: {
    //  事件监听相关的方法
   tabClick(index){
      switch(index){
        case 0:
          this.currentType = 'pop'
          break
        case 1:
          this.currentType = 'new'
          break
        case 2:
          this.currentType = 'sell'
          break
      }
   },

    // 网络请求相关的方法
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        // console.log(res);
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1
      getHomeGoods(type, page).then( res => {
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
      });
    },
  },
};
</script>


<style scoped>
#home {
  padding-top: 44px;
}
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9;
}

.tab-control {
  position: sticky;
  top: 44px;
  z-index: 9;
}
.content{
  /* color:red; */
  height: 300px;
  overflow: hidden;
}
</style>


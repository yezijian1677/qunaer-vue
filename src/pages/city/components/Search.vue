<template>
  <div>
    <div class="search">
      <input
        v-model="keyword"
        class="search-input"
        type="text"
        placeholder="输入城市名"
      />
    </div>
    <div class="search-content" ref="search" v-show="keyword">
      <ul>
        <li
          v-for="item of list"
          @click="handleCityClick(item.name)"
          :key="item.id"
          class="search-item border-bottom"
        >
          {{ item.name }}
        </li>
        <li v-show="hasNoData" class="search-item border-bottom">
          没有匹配数据
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Bscroll from "better-scroll";
import { mapState, mapMutations } from "vuex";

export default {
  name: "CitySearch",
  props: {
    cities: Object
  },
  data() {
    return {
      keyword: "",
      list: [],
      timer: null
    };
  },
  mounted() {
    this.scroll = new Bscroll(this.$refs.search);
  },
  watch: {
    keyword() {
      if (this.timer) {
        clearTimeout(this.timer);
      }
      if (!this.keyword) {
        this.list = [];
        return;
      }
      this.timer = setTimeout(() => {
        const result = [];
        for (let i in this.cities) {
          this.cities[i].forEach(value => {
            if (
              value.spell.indexOf(this.keyword) > -1 ||
              value.name.indexOf(this.keyword) > -1
            ) {
              result.push(value);
            }
          });
        }
        this.list = result;
      }, 100);
    }
  },
  computed: {
    hasNoData() {
      return !this.list.length;
    }
  },
  methods: {
    handleCityClick(city) {
      this.changeCity(city);
      this.$router.push("/");
    },
    ...mapMutations(["changeCity"])
  }
};
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl';
    .search
        height .72rem
        padding 0 .1rem
        background $bgColor
        .search-input
            box-sizing border-box
            width 100%
            height .62rem
            line-height .62rem
            text-align center
            border-radius .06rem
            padding 0 .1rem
    .search-content
        z-index 1
        position absolute
        overflow hidden
        top 1.58rem
        left 0
        right 0
        bottom 0
        background #eee
        .search-item
            line-height .62rem
            padding-left .2rem
            background #ffffff
            color #666
</style>

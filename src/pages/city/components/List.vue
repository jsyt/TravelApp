<template>
  <div class="list" ref="wrapper">
    <div>
      <div class="area">
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
            <div class="button">{{this.city}}</div>
          </div>
        </div>
      </div>
      <div class="area">
        <div class="title border-topbottom">热门城市</div>
        <div class="button-list">
          <div class="button-wrapper" v-for="item of hotCities" :key="item.id" @click="handleCityClick(item.name)">
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>
      <div class="area" v-for="(items, key) of cities" :key='key' :ref="key">
        <div class="title border-topbottom">{{key}}</div>
        <div class="item-list" v-for="item of items" :key=item.id @click="handleCityClick(item.name)">
          <div class="item border-bottom">{{item.name}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'

export default {
  name: 'CityList',
  props: {
    cities: Object,
    hotCities: Array,
    letter: String
  },
  computed: {
    ...mapState(['city'])
  },
  mounted: function () {
    this.scroll = new Bscroll(this.$refs.wrapper)
  },
  watch: {
    letter () {
      if (this.letter) {
        const ele = this.$refs[this.letter][0]
        this.scroll.scrollToElement(ele)
      }
    }
  },
  methods: {
    handleCityClick (city) {
      // this.$store.commit('changeCityMt', city)
      this.changeCityMt(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCityMt'])
  }
}
</script>

<style lang='stylus' scoped>
 @import '~styles/varibles.styl'
  .border-topbottom
    &:before
      border-color : #ccc
    &:after
      border-color : #ccc
  .border-bottom
    &:before
      border-color : #ccc
  .list
    position: absolute;
    overflow: hidden;
    top: 1.58rem;
    left: 0;
    right: 0;
    bottom: 0;
    .title
      line-height : .54rem;
      background: #eee;
      padding-left : .2rem;
      color: #666;
      font-size : .26rem;
    .button-list
      overflow: hidden;
      padding: .1rem .6rem .1rem .1rem;
      .button-wrapper
        float: left;
        width: 33.33%;
        .button
          margin: .1rem;
          text-align: center;
          border: .02rem solid #ccc;
    .item-list
      .item
        line-height: .76rem;
        padding-left: .2rem;
</style>

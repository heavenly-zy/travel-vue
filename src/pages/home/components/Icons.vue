<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <swiper-slide class="clearfix" v-for="(page,index) of pages" :key="index">
        <div class="icon" v-for="item of page" :key="item.id">
          <div class="img-wrapper">
            <img :src="item.imgAddr" />
          </div>
          <p>{{item.name}}</p>
        </div>
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  name: "HomeIcons",
  props: {
    list: Array
  },
  data() {
    return {
      swiperOption: {
        pagination: {
          el: ".swiper-pagination"
        }
      }
    };
  },
  computed: {
    pages() {
      const pages = [];
      this.list.forEach((item, index) => {
        const page = Math.floor(index / 8);
        if (!pages[page]) {
          pages[page] = [];
        }
        pages[page].push(item);
      });
      return pages;
    }
  }
};
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
@import '~styles/mixins.styl'
.clearfix::after
  content ''
  display block
  clear both
.icons >>> .swiper-container
  width 100%
  height 0
  padding-bottom 58%
.icons
  margin-top 0.2rem
  .icon
    position relative
    width 25%
    height 0
    padding-bottom 25%
    float left
    .img-wrapper
      position absolute
      top 0
      left 0
      right 0
      bottom 0.44rem
      text-align center
      img
        height 100%
    p
      position absolute
      left 0
      right 0
      bottom 0
      height 0.44rem
      line-height 0.44rem
      color $fontColor
      text-align center
      ellipsis()
</style>

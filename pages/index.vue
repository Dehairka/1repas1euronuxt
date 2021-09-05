<template>
  <div class="homePage">
    <div class="homePage_nav">
      <ul class="nav">
        <li>All</li>
        <li class="active">Chicken</li>
        <li>Fish</li>
        <li>Fruits</li>
        <li>Pasta</li>
        <li>Pakistani</li>
        <li>Chinese</li>
      </ul>
      <!-- <div class="swiper-pagination" slot="pagination"></div> -->
    </div>
    <div class="homePage_content">
      <swiper ref="mySwiper" :options="swiperOptions">
      <swiper-slide v-for="(plat, index) in plats" :key="index">
        <Plat :plat="plat"/>
      </swiper-slide>
      </swiper>
    </div>
  </div>
</template>

<script>
import { Swiper, SwiperSlide, directive } from 'vue-awesome-swiper'
import 'swiper/css/swiper.css'

export default {
  components: {
    Swiper,
    SwiperSlide
  },
  directives: {
    swiper: directive
  },
  layout: 'default',
  data(){
    return {
      plats: [],
      swiperOptions: {
          slidesPerView: 1.5,
          spaceBetween: 300,
          pagination: {
            el: '.swiper-pagination',
            clickable: true
          },
          // Some Swiper option/callback...
        }
    }
  },
  async fetch() {
    this.plats = await this.$content('plats')
      .fetch()
  },
  computed: {
      swiper() {
        return this.$refs.mySwiper.$swiper
      }
    },
    mounted() {
      this.swiper.slideTo(0, 1000, false)
    },
  methods: {
    imgSrc(nameImg, folder){
      try {
        return require(`~/assets/img/${folder}/${nameImg}`)
      } catch (error) {
        return null
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.homePage{
  height: 100%;

  &_content{
    display: flex;
    justify-content: space-between;
    height: 80vh;
  }

  .nav{
    display: flex;
    width: 50%;
    justify-content: space-around;
    font-size: 1.3em;
    font-weight: 600;
    color: rgba(0,0,0,0.5);

    .active, li:hover{
      color: $black;
      cursor: pointer;
    }
  }

}
</style>

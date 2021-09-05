<template>
  <div class="homePage">
    <div class="homePage_nav">
      <ul class="nav">
        <li :class="sectionActivated == 'all' ? 'active' : ''" @click="changeSection('all')">All</li>
        <li :class="sectionActivated == 'chicken' ? 'active' : ''" @click="changeSection('chicken')">Chicken</li>
        <li :class="sectionActivated == 'fish' ? 'active' : ''" @click="changeSection('fish')">Fish</li>
        <li :class="sectionActivated == 'fruit' ? 'active' : ''" @click="changeSection('fruit')">Fruits</li>
        <li :class="sectionActivated == 'pasta' ? 'active' : ''" @click="changeSection('pasta')">Pasta</li>
        <li :class="sectionActivated == 'pakistani' ? 'active' : ''" @click="changeSection('pakistani')">Pakistani</li>
        <li :class="sectionActivated == 'chinese' ? 'active' : ''" @click="changeSection('chinese')">Chinese</li>
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
      sectionActivated: 'all',
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
    this.plats = await this.$content('plats', {deep:true})
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
    },
    async changeSection(section){
      this.sectionActivated = section
      if(section !== 'all'){
        this.plats = await this.$content('plats/'+section)
          .fetch()
      }else{
        this.plats = await this.$content('plats', { deep: true })
          .fetch()
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

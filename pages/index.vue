<template>
  <div class="homePage">
    <div class="homePage_nav">
      <ul class="nav">
        <li :class="sectionActivated == 'all' ? 'active' : ''" @click="changeSection('all')">Tout</li>
        <li :class="sectionActivated == 'chicken' ? 'active' : ''" @click="changeSection('chicken')">Poulet</li>
        <li :class="sectionActivated == 'fish' ? 'active' : ''" @click="changeSection('fish')">Poisson</li>
        <li :class="sectionActivated == 'fruit' ? 'active' : ''" @click="changeSection('fruit')">Fruits</li>
        <li :class="sectionActivated == 'pasta' ? 'active' : ''" @click="changeSection('pasta')">Pâtes</li>
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
    <div class="homePage_feature">
      <h3>A voir également</h3>
      <div class="homePage_feature_content">
        <div v-for="(feature, index) in 6" :key="index" class="feature">
          <img :src="require('@/assets/img/features/00'+index+'.png')" alt="feature img">
          <h4>Générateur de repas</h4>
          <span>1€ par repas</span>
        </div>
      </div>
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

  &_feature{

    &_content{
      display: flex;
      justify-content: space-around;
      align-items: center;
    }
    h3{color:rgba(0,0,0,0.5); font-style: italic;}
  }

  .feature{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    background-color: $primary;
    border: 4px solid white;
    border-radius: 16px;
    width: 12%;
    min-width: 150px;
    margin-top: 40px;
    position: relative;
    padding: 8px;

    img{
      position: relative;
      top: -50px;
      width: 100%;
    }
    h4, span{
      position: relative;
      top: -50px;
    }
    span{
      color: rgba(0,0,0,0.5);
      margin-top: 8px;
    }
  }

}
</style>

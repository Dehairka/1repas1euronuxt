<template>
  <div class="platPage">

  </div>
</template>

<script>

export default {
  layout: 'default',
  data(){
    return {
      plats: []
    }
  },
  async fetch() {
    this.plats = await this.$content('plats')
      .fetch()
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

</style>

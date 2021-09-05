<template>
  <div class="plat">
          <img v-if="plat.img" class="plat_img" :src="imgSrc(plat.img, 'plats')" alt="Image plat">
          <h2 class="plat_title"><NuxtLink :to="/plats/+plat.section+'-'+plat.slug">{{plat.title}}</NuxtLink></h2>
          <p class="plat_description">{{plat.description}}</p>

        <div class="plat_ingredients">
          <h3>Ingrédients</h3>
          <div class="plat_ingredients_content">
            <div v-for="(ingredient, indexIng) in plat.ingredients" :key="indexIng" class="ingredient">
              <div class="ingredient_img">
                <img :src="imgSrc(ingredient.img, 'icons')" alt="Svg icon">
              </div>
              <div class="ingredient_content">
                <div class="ingredient_title">
                  {{ingredient.title}}
                </div>
                <span class="ingredient_quantity">
                  {{ingredient.quantity}}
                </span>
              </div>
            </div>
          </div>
          <NuxtLink :to="/plats/+plat.section+'-'+plat.slug"><input class="btn" type="button" value="Voir tous les ingrédients"></NuxtLink>
        </div>

        <div class="plat_nutritionals">
          <h3>Nutritions</h3>
          <div class="plat_nutritionals_content">
            <div v-for="(nutrition, indexNut) in plat.nutritionals" :key="indexNut" class="nutrition">
              <strong class="nutrition_number">
                {{nutrition.number}}
              </strong>
              <strong class="nutrition_title">
                {{nutrition.title}}
              </strong>
              <span class="nutrition_value">
                {{nutrition.value}}
              </span>
            </div>
          </div>
          <NuxtLink :to="/plats/+plat.section+'-'+plat.slug"><input class="btn" type="button" value="Voir la recette"></NuxtLink>
          <input class="btn--fill" type="button" value="Ajouter aux favoris">
        </div>
        </div>
</template>

<script>
export default {
  name: 'plat',
  props: {
    plat: Object
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
.plat{
    margin-top: 32px;
    padding: 8px;
    position: relative;
    background-color: $primary;
    border: 8px solid white;
    width: 50vw;
    min-height: 40vh;
    height: 85%;
    border-radius: 16px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    cursor: auto;
    box-shadow: 2px 2px 10px rgba(0,0,0,0.3);

  p{
    width: 70%;
  }
  h3{
    color: rgba(0,0,0,0.5);
    font-weight: 600;
    font-style: italic;
    margin-top: 16px;
  }

    &_img{
      position: absolute;
      right: -15vw;
      top: 0vh;
      width: 35vw;
      // z-index: 5;
    }

    &_ingredients{

      &_content{
        display: flex;
        flex-wrap: wrap;
        width: 80%;
      }
      input{
        margin-top: 8px;
      }
      .ingredient{
        // background-color: grey;
        width: 40%;
        display: flex;
        position: relative;
        margin-top: 8px;

        &_img{
          background-color: $primary;
          border: solid 2px white;
          border-radius: 8px;
          padding: 8px;
        }
        &_title{
          font-weight: 600;
          padding-top: 8px;
          padding-left: 8px;
        }
        &_quantity{
          color: rgba(0,0,0,0.5);
          padding-left: 8px;
        }
      }
    }

    &_nutritionals{
      width: 80%;
      &_content{
        display: flex;
      }
      .nutrition{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: $primary;
        border-radius: 8px;
        border: solid 2px white;
        width: 10%;
        padding: 16px;
        margin: 8px;
        margin-left: 0px;
      }
    }
  }
</style>
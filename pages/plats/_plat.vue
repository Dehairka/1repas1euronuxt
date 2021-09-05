<template>
  <div class="platPage plat">
    <img v-if="plat.img" class="plat_img" :src="imgSrc(plat.img, 'plats')" alt="Image plat">
          <h2 class="plat_title">{{plat.title}}</h2>
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
          <input class="btn" type="button" value="Voir tous les ingrédients">
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
          <input class="btn" type="button" value="Recette">
          <input class="btn--fill" type="button" value="Ajouter aux favoris">
        </div>

        <div class="plat_instructions">
          <h3>Instructions de préparation</h3>
          <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Consequuntur officiis perspiciatis quis numquam eum repudiandae inventore eius aliquid iusto ab nisi, ad amet. Eveniet veritatis ratione nobis. Suscipit, tenetur itaque.</p>
          <div v-for="(step, index) in 3" :key="index" class="step">
            <h4>Étape {{index+1}}</h4>
            <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Voluptas repudiandae obcaecati consequatur, facilis placeat cumque assumenda temporibus sapiente esse, fugiat qui enim accusantium, dolorem exercitationem! Laudantium sunt numquam qui repellat?</p>
          </div>          
        </div>
  </div>
</template>

<script>

export default {
  layout: 'defaultWithoutNav',
  data(){
    return {
      plat: []
    }
  },
  async fetch() {
    const params = this.$route.params.plat.split("-")
    this.plat = await this.$content('plats/'+params[0]+'/'+params[1])
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
.plat{
    margin-top: 32px;
    padding: 8px;
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 100%;
    margin: auto;

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
      width: 35vw;
      right: 0;
      top: 0;
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

.step{
  margin: 8px;
  margin-left: 0px;
}
</style>

<template>
  <div class="homePage">
    <ul class="nav">
      <li>All</li>
      <li class="active">Chicken</li>
      <li>Fish</li>
      <li>Fruits</li>
      <li>Pasta</li>
      <li>Pakistani</li>
      <li>Chinese</li>
    </ul>
    <div class="homePage_content">
      <div v-for="(plat, index) in plats" :key="index" class="plat">
      <div class="plat_background">
        <img v-if="plat.img" class="plat_img" :src="plat.img" alt="Image plat">
        <h2 class="plat_title">{{plat.title}}</h2>
        <p class="plat_description">{{plat.description}}</p>

      <div class="plat_ingredients">
        <h3>Ingrédients</h3>
        <div v-for="(ingredient, indexIng) in plat.ingredients" :key="indexIng" class="ingredient">
          <div class="ingredient_img">
            ok
          </div>
          <div class="ingredient_title">
            {{ingredient.title}}
          </div>
          <div class="ingredient_quantity">
            {{ingredient.quantity}}
          </div>
        </div>
        <input class="btn" type="button" value="Voir tous les ingrédients">
      </div>

      <div class="plat_nutritionals">
        <h3>Nutritions</h3>
        <div v-for="(nutrition, indexNut) in plat.nutritionals" :key="indexNut" class="nutrition">
          <div class="nutrition_title">
            {{nutrition.title}}
          </div>
        </div>
        <input class="btn" type="button" value="Recette">
        <input class="btn--fill" type="button" value="Ajouter aux favoris">
      </div>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  layout: 'default',
  data(){
    return {
      plats: [
        {
          title: "Chicken Steak",
          description: "Lorem, ipsum dolor sit amet consectetur adipisicing elit. Id quibusdam, dolore totam earum eveniet accusamus ipsam autem quidem cum deleniti temporibus ducimus molestiae quae placeat. Dolores architecto odit voluptatibus impedit.",
          img: require('@/assets/img/plats/001.png'),
          ingredients: [
            {
              img: null,
              title: "Chicken",
              quantity: "1 Chicken Breast piece"
            },
            {
              img: null,
              title: "Chicken",
              quantity: "1 Chicken Breast piece"
            },
            {
              img: null,
              title: "Chicken",
              quantity: "1 Chicken Breast piece"
            },
            {
              img: null,
              title: "Chicken",
              quantity: "1 Chicken Breast piece"
            }
          ],
          nutritionals: [
            {
              number: "350",
              title: "Calories",
              value: "Kcal"
            },
            {
              number: "350",
              title: "Calories",
              value: "Kcal"
            },
            {
              number: "350",
              title: "Calories",
              value: "Kcal"
            },
            {
              number: "350",
              title: "Calories",
              value: "Kcal"
            },
          ]
        }
      ]
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

  .plat{
    margin-top: 32px;
    padding: 8px;
    position: relative;
    background-color: white;
    width: 50vw;
    border-radius: 16px;

    &_img{
      position: absolute;
      right: -30%;
      top: 0;
      width: 35vw;
      // z-index: 5;
    }
  }
  .plat_background{
    background-color: $primary;
    border-radius: 16px;
    padding: 24px;
    position: relative;
  }
  p{
    width: 70%;
  }

}
</style>

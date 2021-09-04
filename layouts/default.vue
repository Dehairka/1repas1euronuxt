<template>
  <div class="layoutDefault">
      <div class="layoutDefault_topNav">
          <img width="170" :src="require('@/assets/img/logo.png')" alt="logo">
      </div>
      <div class="layoutDefault_content">
          <ul class="nav">
              <li>Breakfast</li>
              <li class="active">Lunch</li>
              <li>Dinner</li>
          </ul>
          <div class="content">
            <Nuxt />
          </div>
      </div>
  </div>
</template>

<script>
export default {
}
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&display=swap');

.layoutDefault{
    background-color: $primary;
    border-radius: 24px;
    position: relative;
    font-family: 'Lato', sans-serif;

    &_topNav{
        width: 100%;
        height: 7%;
        // background-color: grey;
        padding: 16px;
    }

    &_content{
        height: 85%;
        display: flex;
        overflow-x: visible;
        overflow-y: hidden;

        .nav{
            margin: auto;
            width: 10%;
            height: 80vh;
            display: flex;
            justify-content: space-around;
            flex-direction: column;
            align-items: center;
            position: relative;
            li{
                transform: rotate(270deg);
                color: rgba(0,0,0,0.5);
                font-weight: 600;
                font-size: 1.3em;
                position: relative;
            }
            li.active::after, li:hover::after{
                content: ' ';
                white-space: pre;
                background-color: $secondary;
                width: 5px;
                height: 5px;
                position: absolute;
                padding: 5px;
                top: 25px;
                right: 40%;
                border-radius: 20px;
            }
            li.active, li:hover{
                color: $black;
                cursor: pointer;
            }
        }
        .content{
            padding: 24px;
            width: 90%;
        }
    }
}
</style>
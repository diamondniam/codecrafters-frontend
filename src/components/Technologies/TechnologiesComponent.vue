<script setup lang="ts">
import SubcontentsElement from '@/components/Technologies/SubcontentsElement.vue'
import TechnologiesAnimations from '@/components/Technologies/TechnologiesAnimations.vue'
import type Technology from '@/components/Technologies/TechnologyInterface'
import { useApi } from '@/stores/api'

const api = useApi()
const technologies: Technology[] = await api.getData('technologies')
</script>

<template>
  <div class="container" id="technologies">
    <TechnologiesAnimations />

    <div class="gradient"></div>
    <div class="gradient"></div>

    <div class="title title-desktop">
      Используем новейшие скоростные технологии.
    </div>

    <div class="title title-mobile">
      Новейшие технологии.
    </div>

    <div class="content">
      <div class="image">
        <img class="main-image-desktop" src="../../assets/images/technologies/cpu.svg" alt="Главная картинка">
        <img class="main-image-mobile" src="https://imgur.com/cZN5VGy.png" alt="Главная картинка">
        <div class="blur blur-1"></div>
        <div class="blur blur-2"></div>
        <div class="blur blur-3"></div>
      </div>

      <div class="boxes">
        <div class="border-gradient border-gradient-vue">
          <div class="box box-vue">
            <img :src="technologies[0].image" alt="Картинка технологии">
            <div class="box-bottom">
              <div class="box-title">{{ technologies[0].title }}</div>
              <div class="box-text">{{ technologies[0].description }}</div>
            </div>
          </div>
        </div>

        <div class="border-gradient border-gradient-express">
          <img class="mobile-lines lines-express" :src="technologies[1].mobileLines" alt="Картинка технологии">
          <div class="box box-express">
            <img :src="technologies[1].image" alt="Картинка технологии">
            <div class="box-bottom">
              <div class="box-title">{{ technologies[1].title }}</div>
              <div class="box-text">{{ technologies[1].description }}</div>
            </div>
          </div>
        </div>

        <div class="border-gradient border-gradient-mongodb">
          <img class="mobile-lines lines-mongodb" :src="technologies[2].mobileLines" alt="Картинка технологии">
          <div class="box box-mongodb">
            <img :src="technologies[2].image" alt="Картинка технологии">
            <div class="box-bottom">
              <div class="box-title">{{ technologies[2].title }}</div>
              <div class="box-text">{{ technologies[2].description }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <SubcontentsElement :technologies="technologies" />

  </div>
</template>

<style scoped lang="scss">
@import "../../assets/styles/colors";

.container {
  height: 100%;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: start;
  gap: 70px;
  background: $dark-2;
  width: 100%;
  overflow: hidden;
  position: relative;
}

.gradient {
  width: 100%;
  height: 100%;
  position: absolute;
  z-index: 100;
  pointer-events: none;
}

.gradient:nth-child(1) {
  background: linear-gradient(to right, $dark-2, rgba($dark-2, 0) 15%);
}

.gradient:nth-child(2) {
  background: linear-gradient(to left, $dark-2, rgba($dark-2, 0) 15%);
}

.blur {
  position: absolute;
  width: 300px;
  height: 300px;
  background: rgba($dark-2, .5);
  left: -100px;
  top: -50px;
  backdrop-filter: blur(5px);
  mask-image: radial-gradient(rgba($dark-2, 1), rgba($dark-2, 0) 80%);
  pointer-events: none;
}

.blur-2 {
  left: auto;
  top: -20px;
  right: -100px;
}

.blur-3 {
  left: 45%;
}

.title {
  font-size: 50px;
  line-height: 45px;
  width: 700px;
  background: linear-gradient(-100deg, $gradient-6);
  background-clip: text;
  -webkit-text-fill-color: transparent;
  position: relative;
  margin-top: 7%;
}

.title-mobile {
  display: none;
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  z-index: 10;

  .image {
    width: 55%;
    position: relative;

    img {
      transform: translateX(-5px);
      width: 100%;
      display: block;
    }

    .main-image-mobile {
      display: none;
    }
  }

  .boxes {
    display: flex;
    justify-content: center;
    gap: 6.5%;
    width: 100%;
    margin-bottom: 10%;

    .mobile-lines {
      display: none;
    }

    .border-gradient {
      box-sizing: border-box;
      width: 20%;
      height: 330px;
      border-radius: 30px;
      padding: .06em;

      .box {
        background: $dark-1;
        width: 100%;
        height: 100%;
        border-radius: 30px;
        box-sizing: border-box;
        padding: 20px;
        mask-size: 200%;

        img {
          height: 70px;
          margin-bottom: 20px;
        }

        .box-title {
          font-size: 30px;
          margin-bottom: 10px;
        }

        .box-text {
          font-weight: 300;
          font-size: 16px;
          line-height: 20px;
        }
      }

      .box-vue {
        .box-title { color: #1cbd93; }
        .box-text { color: #79978f; }
        img { width: 90px }
        mask-image: linear-gradient(-80deg, rgba(255, 255, 255, 0.9) 10%, #ffffff 30%, rgba(255, 255, 255, 0.9) 90%);
      }

      @keyframes shine {
        from { mask-position: 150%; }
        to { mask-position: -50%; }
      }

      .box-express {
        .box-title { color: #d5da3a; }
        .box-text { color: #939378; }
        img { width: 100px; height: auto }
        mask-image: linear-gradient(-90deg, rgba(255, 255, 255, 0.9) 10%, #ffffff 50%, rgba(255, 255, 255, 0.9) 90%);
      }

      .box-mongodb {
        .box-title { color: #2dbacf; }
        .box-text { color: #758c8e; }
        img { height: 85px }
        mask-image: linear-gradient(-70deg, rgba(255, 255, 255, 0.9) 10%, #ffffff 70%, rgba(255, 255, 255, 0.9) 90%);
      }
    }

    .border-gradient-vue {
      background: linear-gradient(200deg, $gradient-7);
      box-shadow: 0 3px 3px 0 rgba(15, 92, 71, 0.51);
    }

    .border-gradient-express {
      background: linear-gradient(50deg, $gradient-8);
      box-shadow: 0 3px 3px 0 rgb(66, 66, 45);
    }

    .border-gradient-mongodb {
      background: linear-gradient(220deg, $gradient-9);
      box-shadow: 0 3px 3px 0 rgb(50, 83, 87);
    }
  }
}


@media only screen and (max-width: 900px) {
  .container {
    height: 100%;
    gap: 50px;
  }

  .blur {
    display: none;
  }

  .title {
    width: 300px;
    margin-top: 20%;
  }

  .title-desktop {
    display: none;
  }

  .title-mobile {
    display: block;
  }

  .content {
    .image {
      width: 150%;
      position: relative;

      .main-image-desktop {
        display: none;
      }

      .main-image-mobile {
        display: block;
      }
    }

    .boxes {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      gap: 6.5%;
      width: 100%;
      position: relative;

      .mobile-lines {
        display: block;
        position: absolute;
        width: 50%;
      }

      .box {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
      }

      .lines-express {
        top: 47%;
        left: -35%;
      }

      .lines-mongodb {
        top: 80%;
        right: -35%;
      }

      .border-gradient {
        box-sizing: border-box;
        width: 70%;
        border-radius: 30px;
        padding: .06em;
        margin-bottom: 30px;
      }

      .border-gradient-vue {
        background: linear-gradient(200deg, $gradient-7);
        box-shadow: 0 3px 3px 0 rgba(15, 92, 71, 0.51);
      }

      .border-gradient-express {
        background: linear-gradient(50deg, $gradient-8);
        box-shadow: 0 3px 3px 0 rgb(66, 66, 45);
      }

      .border-gradient-mongodb {
        background: linear-gradient(220deg, $gradient-9);
        box-shadow: 0 3px 3px 0 rgb(50, 83, 87);
      }
    }
  }
}

@media only screen and (max-width: 600px) {
  .title {
    line-height: 32px;
    font-size: 35px;
  }

  .content {
    .boxes {
      .border-gradient {
        height: 330px;
      }
    }
  }
}
</style>
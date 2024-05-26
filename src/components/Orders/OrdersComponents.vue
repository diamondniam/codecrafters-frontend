<script setup lang="ts">
import {ref, onMounted} from "vue";
import axios from "axios";

interface Order {
  id?: string;
  image: string;
  title: string;
  link: string;
}

const orders = ref<Order[]>([
  {image: '', title: '', link: ''},
  {image: '', title: '', link: ''},
  {image: '', title: '', link: ''},
  {image: '', title: '', link: ''},
  {image: '', title: '', link: ''},
])

const loadOrders = async () => {
  try {
    const response = await axios.get('http://localhost:3000/orders')
    orders.value = response.data
  } catch (error) {
    console.error('Ошибка при загрузке заказов:', error)
  }
}

onMounted(() => {
  loadOrders()
})
</script>

<template>
  <div class="container">
    <div class="title">Нас выбирают.</div>

    <div class="wrapper">
      <div class="images left">
        <div class="border b1">
          <div class="box i1" :style="{backgroundImage: `url(${orders[0].image})`}"></div>
          <a class="link l1" target="_blank" :href="orders[0].link">
            <div>{{orders[0].title}}</div>
            <span></span>
            <img src="../../assets/images/link-arrow.svg" alt="">
          </a>
        </div>
        <div class="border b2">
          <div class="box i2" :style="{backgroundImage: `url(${orders[1].image})`}"></div>
          <a class="link l2" target="_blank" :href="orders[0].link">
            <div>{{orders[1].title}}</div>
            <span></span>
            <img src="../../assets/images/link-arrow.svg" alt="">
          </a>
        </div>
      </div>

      <div class="images right">
        <div class="border b3">
          <div class="box i3" :style="{backgroundImage: `url(${orders[2].image})`}"></div>
          <a class="link l3" target="_blank" :href="orders[0].link">
            <div>{{orders[2].title}}</div>
            <span></span>
            <img src="../../assets/images/link-arrow.svg" alt="">
          </a>
        </div>

        <div class="images-group">
          <div class="border b4">
            <div class="box i4" :style="{backgroundImage: `url(${orders[3].image})`}"></div>
            <a class="link l4" target="_blank" :href="orders[0].link">
              <div>{{orders[3].title}}</div>
              <span></span>
              <img src="../../assets/images/link-arrow.svg" alt="">
            </a>
          </div>
          <div class="border b5">
            <div class="box i5" :style="{backgroundImage: `url(${orders[4].image})`}"></div>
            <a class="link l5" target="_blank" :href="orders[0].link">
              <div>{{orders[4].title}}</div>
              <span></span>
              <img src="../../assets/images/link-arrow.svg" alt="">
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
@import "../../assets/styles/colors";

.container {
  min-height: 100vh;
  overflow: hidden;
  width: 100%;
  height: 1300px;
  display: flex;
  flex-direction: column;
  align-items: center;
  mask-image: linear-gradient(to top, rgba($dark-2, 0), rgba($dark-2, 1) 40%);
}

.title {
  font-size: 50px;
  background: linear-gradient(-170deg, $gradient-5);
  background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-bottom: 50px;
}

.wrapper {
  display: flex;
  width: 400%;
  justify-content: center;
  background: #1f1f1f;
  padding: 20px;

  .images {
    display: flex;
    flex-direction: column;
    width: 50%;

    .images-group {
      display: flex;
      align-items: start;
      width: 50%;
    }

    .border {
      box-sizing: border-box;
      border: 1px dotted rgba(255, 255, 255, 0.2);
      padding: 20px;
      width: 100%;
      position: relative;

      .box {
        border-radius: 10px;
        background-repeat: repeat;
        background-size: contain;
        width: 100%;
        height: 350px;
        transition: opacity 1s;
        display: flex;
        justify-content: end;
        align-items: center;

        a {
          display: inline-block;
        }
      }

      .link {
        position: absolute;
        display: flex;
        background: rgba(0, 0, 0, 0.4);
        backdrop-filter: blur(10px);
        top: 45%;
        right: 10%;
        border: 1px solid black;
        border-radius: 30px;
        overflow: hidden;
        text-decoration: none;
        color: white;
        cursor: pointer;
        opacity: 0;
        transition: all .7s;

        span {
          width: 1px;
          background: white;
        }

        div {
          padding: 10px 20px;
          font-weight: 300;
        }

        img {
          margin: 0 20px;
        }
      }

      // LINKS
      .l2 {
        top: 25%;
        right: 10%;
      }

      .l3 {
        right: auto;
        left: 10%;
      }

      .l4 {
        right: auto;
        left: 25%;
        top: 30%;
      }

      .l5 {
        right: auto;
        top: 30%;
        left: 20%;
      }

      // IMAGES
      .i1 {
        background-position: right;
        height: 90vh;
      }

      .i2 {
        height: 600px;
        background-position: right top;
        background-size: contain;
      }

      .i3 {
        height: 65vh;
        width: 70vw;
        background-position: left top;
        background-size: contain;
      }

      .i4 {
        height: 1000px;
        background-position: left top;
        background-size: contain;
      }

      .i5 {
        height: 1000px;
        background-position: left top;
        background-size: contain;
      }

      &:hover .box {
        opacity: .5;
      }

      &:hover .link {
        opacity: 1;
        filter: blur(0px);
      }
    }

    // BORDERS
    .b2 {
      border-top: 0;
    }

    .b3, .b4 {
      border-left: 0;
      border-bottom: 0;
      border-right: 0;
    }

    .b4, .b5 {
      width: 400px;
    }
  }
}
</style>
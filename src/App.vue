<template>
  <main id="app" @mousemove="mousemove">
    <section class="products">
      <Product 
        v-for="product in products"
        :key="product.color"
        :product="product"
      />
    </section>
  </main>
</template>

<script>
import Product from './components/Product';

export default {
  name: 'App',
  components: {
    Product
  },
  data() {
    return {
      products: [
        {
          title: 'ポップコーン',
          color: 'green',
          bgtext: 'SALT',
          src: require('./assets/popcorn.png')
        },
        {
          title: 'ビール',
          color: 'blue',
          bgtext: 'BEER',
          src: require('./assets/beer_img.png')
        },
        {
          title: '映画館',
          color: 'pink',
          bgtext: 'MOVIE',
          src: require('./assets/camera.png')
        }
      ]
    }
  },
  methods: {
    mousemove(e) {
      let mouseX = e.clientX;
      let mouseY = e.clientY;
      let products = document.querySelectorAll('.products .product');
      for (let i = 0; i < products.length; i++) {
        let product = products[i];
        let product_image = product.querySelector('.product-image-wrap');
        let img_x = mouseX - this.coords(product_image).x;
        let img_y = mouseY - this.coords(product_image).y;
        product_image.style.transform = `translateY(-${img_y/40}px) translateX(-${img_x/40}px) translateZ(100px)`;
        let bgtext = product.querySelector('.bg-text');
        let bg_x = mouseX - this.coords(bgtext).x;
        bgtext.style.transform = `translateX(${bg_x/25}px)`;
      }
    },
    coords (el) {
      let coords = el.getBoundingClientRect();
      return {
        x: coords.left / 2,
        y: coords.top / 2
      }
    }
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body {
    font-family: 'montseratt', sans-serif;
  }
  main {
    width: 100vw;
    min-height: 100vh;
    overflow: hidden;
    background-color: #EEE;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .products {
    display: flex;
    max-width: 1280px;
    padding: 25px;
    margin: 0 auto;
  }
</style>
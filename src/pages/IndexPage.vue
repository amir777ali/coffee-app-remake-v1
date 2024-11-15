<template>
    <q-page class="flex flex-center bg-darkk text-white" >
    <q-card class="text-center q-pa-md card" flat bordered >
      <div class="box1">
        <q-card-section>
        <h2 class="text-h2 text-weight-bold">Start your day <br> with a black <span class="text-orange">coffee</span></h2>
        <p class="text-grey-5 text-weight-medium">
          Choose and taste delicious coffee from the best beans
        </p>
      </q-card-section>
      <q-card-actions  align="center">
        <q-btn class="q-ml-mdb" label="Order Now" to="#PRODUCTS" style="background-color: #CB863F; width: 150px; font-weight: 600;" />
        <q-btn outline  label="Learn About Us" to="#ABOUT" class="q-ml-md" style="color: #6C4620; width: 150px; font-weight: 600;" />
      </q-card-actions>
      </div>
      <q-img src="public/icons/images/cup.png" class="pic"/>
    </q-card>

  </q-page>


<div class="container">
  <div class="q-pa-md row justify-center container-c">
  <q-card v-for="product in topics.populars" :key="product.name" class="My-card ">
    <q-img :src="`public/icons/images/${product.pic}.jpg`" class="rounded-borders" />
    <q-card-section>
      <div class="text-h5 text-weight-medium">{{ product.name }}</div>
      <div class="text-subtitle1 text-grey text-overline">{{ product.des }}</div>
      <div class="text-subtitle2  text-orange-7">${{ product.price }}</div>
    </q-card-section>
    <q-card-actions align="left">
      <q-btn icon="add_shopping_cart"  label="Add to Cart" class="addC" style="background-color: #CB863F; font-weight: 600;"/>
    </q-card-actions>
  </q-card>
  <!-- <q-space></q-space> -->
</div>
<div class="q-pa-md row justify-center container-c">
  <q-card v-for="product in topics.bestSellers" :key="product.name" class="My-card ">
    <q-img :src="`public/icons/images/${product.pic}.jpg`" class="rounded-borders" />
    <q-card-section>
      <div class="text-h5 text-weight-medium">{{ product.name }}</div>
      <div class="text-subtitle1 text-grey text-overline ">{{ product.des }}</div>
      <div class="text-subtitle2 text-orange-7">${{ product.price }}</div>
    </q-card-section>
    <q-card-actions align="left">
      <q-btn icon="add_shopping_cart"  label="Add to Cart"  class="addC" style="background-color: #CB863F; font-weight: 600;"/>
    </q-card-actions>
  </q-card>
</div>
</div>

</template>


<script>
import { ref, reactive } from 'vue'

export default {
  setup() {
    const primary = "#CB863F"
    const basket = ref(JSON.parse(localStorage.getItem('basket')) || [])
    const topics = reactive({
      populars: [
        { name: 'Esperesso Coffee', des: 'with milk', price: 5.0, pic: 'E' },
        { name: 'Latte Coffee', des: 'with milk', price: 7.5, pic: 'L' },
        { name: 'Cappuccino Coffee', des: 'with chocolate', price: 6.2, pic: 'C' },
      ],
      bestSellers: [
        { name: 'Americano Coffee', des: 'with milk', price: 10.3, pic: 'A' },
        { name: 'Macchiato Coffee', des: 'with cream', price: 8.5, pic: 'M' },
        { name: 'Mocha', des: 'with oat cream', price: 11.2, pic: 'MC' }
      ],
    })

    const showCart = () => { /* logic to show cart */ }
    const addToCart = (product) => {
      // logic to add product to basket
    }

    return { basket, topics, showCart, addToCart }
  }
}
</script>

<style>
:root {
  --bg-color: #000000;
  --btn-color: #CB863F;
  --border-color: #6C4620;
  --white: #ffffff;
  --text-gray: #9E9E9E;
}

body {
  background-color: var(--bg-color);
  font-family: "Poppins", sans-serif;
  margin: 0;
  padding: 0;
}

.container-c {
  width: 1400px;
  display: flex;
  gap: 100px;
}

.My-card {
  border-radius: 8px;
  background-color: var(--bg-gray);
  color: var(--white);
  border: 3px solid var(--border-color);

}

.text-orange-7 {
  color: var(--btn-color);
}

.rounded-borders {
  border-radius: 8px;
  border: 3px solid var(--border-color);
  width: 260px;
  height: 260px;
}

.addC {
  font-size: 12px;

}

.text-orange {
  color: #CB863F;
}

.bg-darkk {
  background-color: #000000;
}

.text-grey-5 {
  color: #9E9E9E;
}

.card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: none;
  width: 1400px;
}

.box1 q-btn {
  text-align: center;
}
.pic {
  width: 800px;
}
</style>

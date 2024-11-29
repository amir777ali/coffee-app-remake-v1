<template>
  <q-page class="flex flex-center bg-darkk text-white">
    <q-card class="text-center q-pa-md card" flat bordered>
      <div class="box1">
        <q-card-section>
          <h2 class="text-h2 text-weight-bold">
            Start your day <br />
            with a black <span class="text-orange">coffee</span>
          </h2>
          <p class="text-grey-5 text-weight-medium">
            Choose and taste delicious coffee from the best beans
          </p>
        </q-card-section>
        <q-card-actions align="center">
          <q-btn
            class="q-ml-mdb"
            label="Order Now"
            to="#PRODUCTS"
            style="background-color: #cb863f; width: 150px; font-weight: 600"
          />
          <q-btn
            outline
            label="Learn About Us"
            to="#ABOUT"
            class="q-ml-md"
            style="color: #6c4620; width: 150px; font-weight: 600"
          />
        </q-card-actions>
      </div>
      <q-img src="public/icons/images/cup.png" class="pic" />
    </q-card>
  </q-page>

  <div class="container">
    <div class="q-pa-md row justify-center container-c">
      <q-card
        v-for="product in topics.populars"
        :key="product.name"
        class="My-card"
      >
        <q-img
          :src="`public/icons/images/${product.pic}.jpg`"
          class="rounded-borders"
        />
        <q-card-section>
          <div class="text-h5 text-weight-medium">{{ product.name }}</div>
          <div class="text-subtitle1 text-grey text-overline">
            {{ product.des }}
          </div>
          <div class="text-subtitle2 text-orange-7">${{ product.price }}</div>
        </q-card-section>
        <q-card-actions align="left">
          <q-btn
            icon="add_shopping_cart"
            @click="addToCart(product)"
            label="Add to Cart"
            class="addC"
            style="background-color: #cb863f; font-weight: 600"
          />
        </q-card-actions>
      </q-card>
      <!-- <q-space></q-space> -->
    </div>
    <div class="q-pa-md row justify-center container-c">
      <q-card
        v-for="product in topics.bestSellers"
        :key="product.name"
        class="My-card"
      >
        <q-img
          :src="`public/icons/images/${product.pic}.jpg`"
          class="rounded-borders"
        />
        <q-card-section>
          <div class="text-h5 text-weight-medium">{{ product.name }}</div>
          <div class="text-subtitle1 text-grey text-overline">
            {{ product.des }}
          </div>
          <div class="text-subtitle2 text-orange-7">${{ product.price }}</div>
        </q-card-section>
        <q-card-actions align="left">
          <q-btn
            icon="add_shopping_cart"
            @click="addToCart(product)"
            label="Add to Cart"
            class="addC"
            style="background-color: #cb863f; font-weight: 600"
          />
        </q-card-actions>
      </q-card>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";

const primary = "#CB863F";
const basket = JSON.parse(localStorage.getItem("basket")) || [];
const topics = reactive({
  populars: [
    { name: "Esperesso Coffee", des: "with milk", price: 5.0, pic: "E", count: 0 },
    { name: "Latte Coffee", des: "with milk", price: 7.5, pic: "L", count: 0 },
    { name: "Cappuccino Coffee", des: "with chocolate", price: 6.2, pic: "C", count: 0 },
  ],
  bestSellers: [
    { name: "Americano Coffee", des: "with milk", price: 10.3, pic: "A", count: 0 },
    { name: "Macchiato Coffee", des: "with cream", price: 8.5, pic: "M", count: 0 },
    { name: "Mocha", des: "with oat cream", price: 11.2, pic: "MC", count: 0 },
  ],
});

const addToCart = (product) => {
  // بررسی اینکه آیا محصول در سبد خرید وجود دارد
  const existingProduct = basket.find((item) => item.name === product.name);

  if (existingProduct) {
    // اگر محصول وجود داشت، فقط مقدار count را افزایش بده
    existingProduct.count += 1;
  } else {
    // اگر محصول جدید بود، آن را با count=1 اضافه کن
    basket.push({ ...product, count: 1 });
  }

  // ذخیره سبد خرید در localStorage
  localStorage.setItem("basket", JSON.stringify(basket));
};

</script>

<style>
:root {
  --bg-color: #000000;
  --btn-color: #cb863f;
  --border-color: #6c4620;
  --white: #ffffff;
  --text-gray: #9e9e9e;
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
  color: #cb863f;
}

.bg-darkk {
  background-color: #000000;
}

.text-grey-5 {
  color: #9e9e9e;
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

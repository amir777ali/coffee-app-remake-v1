<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated>
      <q-toolbar class="top">
        <q-btn flat icon="home" to="#top" aria-label="Home" />
        <q-space />
        <q-tabs v-model="tab" align="center">
          <q-tab name="home" label="HOME" to="#HOME" />
          <q-tab name="menu" label="MENU" to="#MENU" />
          <q-tab name="products" label="PRODUCTS" to="#PRODUCTS" />
          <q-tab name="about" label="ABOUT" to="#ABOUT" />
          <q-tab name="contact" label="CONTACT US" to="#CONTACT-US" />
        </q-tabs>
        <q-space />
        <q-btn flat icon="person" />
        <q-btn flat icon="shopping_basket" @click="openCartModal = true" />
      </q-toolbar>
    </q-header>

    <q-dialog v-model="openCartModal">
      <q-card class="q-pa-md card1" style="min-width: 800px">

        <q-card-section>
          <div class="text-h6">YOUR SHOPING CART</div>

          <q-card-section>
            <div>The products added to your cart</div>
            <q-card-section class="card1"></q-card-section>

          </q-card-section>

          <div class="cart-item" style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px">
          <q-card
            flat
            bordered
            class="product-card"
            v-for="(product, index) in basket"
            :key="index"
          >
            <!-- نمایش اطلاعات محصول -->
            <q-card-section class="cart-item-details">
              <div class="text-h6 text1" >{{ product.name }}</div>
              <div class="text-subtitle2 text2">{{ product.des }}</div>
              <div class="text-body1 text-orange-10">{{ product.price }}$</div>
            </q-card-section>

           <div class="cart-item-counter">
            <q-btn
              class="text2"
              flat
              dense
              icon="remove"
              @click="decrementCount(product.name)"
            />
            <span class="item-count">{{ product.count }}</span>
            <q-btn
              class="text2"
              flat
              dense
              icon="add"
              @click="incrementCount(product.name)"
            />
           </div>
          </q-card>
          </div>

        </q-card-section>
        <q-card-actions >
        <q-btn
          flat
          label="close"
          color="primary"
          @click="openCartModal = false"
        />
        <q-btn flat label="pay" color="secondary" />
      </q-card-actions>
      </q-card>


    </q-dialog>


    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer class="text-center">
      <div>تمامی حقوق این صفحه متعلق به بنده است ©</div>
      <q-list> </q-list>
    </q-footer>
  </q-layout>
</template>

<script setup>
import { computed, ref } from "vue";

const basket = ref(
  JSON.parse(localStorage.getItem("basket")) || []
);
const openCartModal = ref(false);

defineOptions({
  name: "MainLayout",
});
const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}

function saveBasket() {
  localStorage.setItem("basket", JSON.stringify(basket.value));
}

function addToBasket(product) {
  const existingProduct = basket.value.find(
    (item) => item.name === product.name
  );

  if (existingProduct) {
    existingProduct.count += 1;
  } else {
    basket.value.push({ ...product, count: 1 });
  }

  saveBasket();
}

function incrementCount(productName) {
  const product = basket.value.find((item) => item.name === productName);
  if (product) {
    product.count += 1;
    saveBasket();
  }
}

function decrementCount(productName) {
  const productIndex = basket.value.findIndex((item) => item.name === productName);

  if (productIndex !== -1) {
    const product = basket.value[productIndex];
    if (product.count > 1) {
      product.count -= 1;
    } else {
      basket.value.splice(productIndex, 1);
    }
    saveBasket();
  }
}
</script>


<style>
.top {
  display: flex;
  justify-content: space-between;
  height: 100px;
  background-color: black;
}


.text1 {
  color: black;
}
.text2 {
  color: #212121;
}

.cart-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border: 2px solid #cb863f;
  border-radius: 8px;
  background-color: #212121;
  color: white;
  margin-bottom: 15px;
}

.cart-item-image {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  margin-right: 10px;
}

.cart-item-details {
  flex-grow: 1;
  margin-right: 10px;
}

.cart-item-name {
  font-size: 1.2rem;
  font-weight: bold;
}

.cart-item-price {
  font-size: 1rem;
  color: #cb863f;
}

.cart-item-counter {
  display: flex;
  align-items: center;
  gap: 8px;
}

.counter-btn {
  color: white;
  border: 1px solid #cb863f;
}

.item-count {
  font-size: 1.2rem;
  font-weight: bold;
  color: black;
}
</style>

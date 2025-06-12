<template>
  <el-container class="mt-10">
    <!-- Products -->
    <el-row class="cards-container" align="middle" justify="space-between">
      <ProductCard
        v-for="(item, index) in productStore.getProducts"
        :key="index"
        :product="item"
        @add-to-cart="onAddToCart"
      />
    </el-row>

    <!-- Cart Drawer as child component -->
    <CartDrawer
      :visible="cartStore.drawerVisible"
      :items="cartStore.items"
      @close="cartStore.toggleDrawer(false)"
      @remove="cartStore.removeFromCart"
    />

    <!-- Footer -->
    <el-footer>
      <el-text>FOOTER</el-text>
    </el-footer>
  </el-container>
</template>

<script setup lang="ts">
import { getProducts } from '@/api/actios/product.action'
import type { ProductTypes } from '@/models/types'
import { useCartStore } from '@/stores/cartStore'
import { useProductStore } from '@/stores/productStore'
import { onMounted } from 'vue'

const productStore = useProductStore()
const cartStore = useCartStore()

function onAddToCart(product: ProductTypes) {
  cartStore.addToCart(product)
  // cartStore.toggleDrawer(true)
}

onMounted(async () => {
  await getProducts()
})
</script>

<style scoped>
.el-container {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.logInSignUpCon {
  display: flex;
  float: right;
  height: 60px;
  width: 10%;
  border-radius: 100px;
  background-color: #dfdfdf;
}

.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  justify-items: center;
  gap: 1em;
  width: 75%;
  padding-bottom: 2em;
}

.el-text {
  color: var(--custom-off-white);
}

.el-footer {
  width: 100%;
  height: 400px;
  background: var(--custom-black);
  padding: 2em;
}
</style>

<template>
  <el-container>
    <!-- Navbar -->
    <el-row style="width: 100%">
      <el-header class="w-full h-[40px] bg-emerald-500 text-white flex items-center">
        <el-row style="width: 100%" align="middle" justify="space-between">
          <el-col :span="2" style="display: flex; align-items: center; gap: 5px">
            <el-icon :size="20"><Phone /></el-icon>
            <el-text style="font-size: 12px; color: white">+639123456789</el-text>
          </el-col>
          <el-col
            :span="20"
            style="display: flex; align-items: center; justify-content: center; gap: 5px"
          >
            <el-text style="color: white">Get 50% off on an selected item | Shop now</el-text>
          </el-col>
          <el-col
            :span="2"
            style="display: flex; align-items: center; justify-content: end; gap: 1.5em"
          >
            <el-dropdown placement="bottom-start">
              <el-row style="gap: 5px; cursor: pointer">
                <el-text style="color: white"> eng </el-text>
                <el-icon :size="15" color="white"><ArrowDown /></el-icon>
              </el-row>
              <template #dropdown>
                <el-dropdown-menu>
                  <el-dropdown-item>The Action 1st</el-dropdown-item>
                  <el-dropdown-item>The Action 2st</el-dropdown-item>
                  <el-dropdown-item>The Action 3st</el-dropdown-item>
                </el-dropdown-menu>
              </template>
            </el-dropdown>
            <el-dropdown placement="bottom-start">
              <el-row style="gap: 5px; cursor: pointer">
                <el-text style="color: white"> Location </el-text>
                <el-icon :size="15" color="white"><ArrowDown /></el-icon>
              </el-row>

              <template #dropdown>
                <el-dropdown-menu>
                  <el-dropdown-item>The Action 1st</el-dropdown-item>
                  <el-dropdown-item>The Action 2st</el-dropdown-item>
                  <el-dropdown-item>The Action 3st</el-dropdown-item>
                </el-dropdown-menu>
              </template>
            </el-dropdown>
          </el-col>
        </el-row>
      </el-header>
    </el-row>

    <!-- Filters -->
    <FilterView />

    <el-row style="width: 75%">
      <el-button type="primary" size="large" class="my-4" @click="openDrawer()"
        >Add New Product</el-button
      >
    </el-row>

    <el-row
      class="cards-container"
      align="middle"
      justify="space-between"
      v-loading="productStore.getLoading"
    >
      <el-col
        v-for="(item, index) in productStore.getProducts"
        :key="index"
        :span="24"
        class="card-container"
      >
        <ProductCard :product="item" />
        <div class="flex justify-end p-2 gap-2">
          <el-button size="small" type="primary" @click="openDrawer(item)">Edit</el-button>
          <el-button size="small" type="danger" @click="removeProduct(item.id)">Delete</el-button>
        </div>
      </el-col>
    </el-row>

    <div
      v-if="productStore.getProducts.length === 0"
      class="w-full flex items-center justify-center"
    >
      <el-empty description="No products found" />
    </div>

    <ProductDrawer
      v-model:visible="drawerVisible"
      :product="selectedProduct"
      @save="saveOrUpdateProduct"
    />
  </el-container>
</template>

<script setup lang="ts">
import { getProducts, deleteProduct, saveProduct } from '@/api/actios/product.action'
import { useProductStore } from '@/stores/productStore'
import { ref, onMounted } from 'vue'
import ProductDrawer from '@/components/ProductDrawer.vue'
import type { ProductTypes } from '@/models/types'

const productStore = useProductStore()
const drawerVisible = ref(false)
const selectedProduct = ref<ProductTypes | null>(null)

onMounted(async () => {
  await getProducts()
})

const openDrawer = (product: ProductTypes | null = null) => {
  selectedProduct.value = product
  drawerVisible.value = true
}

const saveOrUpdateProduct = async (product: ProductTypes) => {
  await saveProduct(product)
}

const removeProduct = async (id: number) => {
  await deleteProduct(id)
}
</script>

<style scoped>
.el-container {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  justify-items: center;
  gap: 1em;
  width: 75%;
  padding-bottom: 2em;
}
</style>

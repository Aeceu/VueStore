<template>
  <el-container>
    <!-- Navbar -->
    <el-row style="width: 100%">
      <el-header class="w-full h-[40px] bg-emerald-500 text-white flex items-center">
        <el-row style="width: 100%" align="middle" justify="space-between">
          <el-col :span="2" style="display: flex; align-items: center; gap: 5px">
            <el-icon :size="20"><Phone /></el-icon>
            <el-text style="font-size: 12px">+639123456789</el-text>
          </el-col>
          <el-col
            :span="20"
            style="display: flex; align-items: center; justify-content: center; gap: 5px"
          >
            <el-text>Get 50% off on an selected item | Shop now</el-text>
          </el-col>
          <el-col
            :span="2"
            style="display: flex; align-items: center; justify-content: end; gap: 1.5em"
          >
            <el-dropdown placement="bottom-start">
              <el-row style="gap: 5px; cursor: pointer">
                <el-text class="text-white"> eng </el-text>
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
                <el-text> Location </el-text>
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

    <!-- Products -->
    <el-row class="cards-container" align="middle" justify="space-between">
      <ProductCard v-for="(item, index) in productStore.getProducts" :key="index" :product="item" />
    </el-row>
  </el-container>
</template>

<script setup lang="ts">
import { getProducts } from '@/api/actios/product.action'
import { useProductStore } from '@/stores/productStore'
import { onMounted } from 'vue'

const productStore = useProductStore()

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

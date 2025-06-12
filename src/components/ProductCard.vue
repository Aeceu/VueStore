<template>
  <el-col :span="24" align="center" justify="center" class="card-container">
    <img :src="product.image" />
    <el-row style="width: 100%; padding: 1em; flex-direction: column" justify="start">
      <el-text class="clamp-1 poppins-semibold" style="width: 100%; text-align: start">{{
        product.title
      }}</el-text>
      <el-text style="width: 100%; text-align: start" size="small">{{ product.category }}</el-text>
      <el-row>
        <el-rate v-model="rate" />
        <el-text style="font-size: 12px" size="small">{{
          `(${product.rating.count} reviews)`
        }}</el-text>
      </el-row>
      <el-text
        style="width: 100%; text-align: start; color: var(--color-green); font-size: 28px"
        size="large"
        class="poppins-bold"
        >{{ `₱ ${product.price}` }}</el-text
      >
      <el-row :gutter="24">
        <el-col :span="24">
          <el-button class="w-full" size="large" type="primary" @click="$emit('edit', product)"
            >Edit</el-button
          >
        </el-col>
        <el-col :span="24">
          <el-button
            class="w-full mt-2"
            size="large"
            type="danger"
            @click="$emit('delete', product.id)"
            >Delete</el-button
          >
        </el-col>
      </el-row>
    </el-row>
  </el-col>
</template>

<script setup lang="ts">
import type { ProductTypes } from '@/models/types'
import { ref } from 'vue'

const props = defineProps<{ product: ProductTypes }>()
defineEmits<{
  (e: 'edit', product: ProductTypes): void
  (e: 'delete', id: number): void
}>()

const rate = ref(Math.floor(props.product.rating.rate))
</script>

<style scoped>
.card-container {
  width: 300px;
  height: 100%;
  box-shadow: 0px 0px 8px 2px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  background: white;
  position: relative;
}
img {
  width: 100%;
  height: 300px;
  padding: 2em;
}
.clamp-1 {
  font-size: 16px;
  line-height: 1.4;
  line-clamp: 1;
  display: -webkit-box;
  -webkit-line-clamp: 1;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
}
.card-button {
  width: fit-content;
  border: 2px solid var(--color-green);
  color: var(--color-green);
  margin-top: 8px;
}

.card-button:hover {
  background: var(--color-green);
  color: white;
  cursor: pointer;
}
</style>

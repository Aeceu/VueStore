<template>
  <el-drawer :before-close="onCancel" v-model="visible" title="Manage Product" size="30%">
    <el-form :model="form" label-width="120px">
      <el-form-item label="Title">
        <el-input v-model="form.title" />
      </el-form-item>
      <el-form-item label="Category">
        <el-input v-model="form.category" />
      </el-form-item>
      <el-form-item label="Price">
        <el-input v-model="form.price" type="number" />
      </el-form-item>
      <el-form-item label="Image URL">
        <el-input v-model="form.image" />
      </el-form-item>
      <el-form-item label="Rating">
        <el-input-number v-model="form.rating.rate" :min="0" :max="5" />
      </el-form-item>
      <el-form-item label="Reviews">
        <el-input-number v-model="form.rating.count" :min="0" />
      </el-form-item>
    </el-form>

    <template #footer>
      <el-button @click="onCancel">Cancel</el-button>
      <el-button type="primary" @click="onSave">Save</el-button>
    </template>
  </el-drawer>
</template>

<script setup lang="ts">
import { reactive, ref, watch, defineEmits } from 'vue'
import type { ProductTypes } from '@/models/types'

const props = defineProps<{
  visible: boolean
  product?: ProductTypes | null
}>()

const emit = defineEmits(['update:visible', 'save'])

const form = reactive<ProductTypes>({
  id: 0,
  title: '',
  description: '',
  price: 0,
  category: '',
  image: '',
  rating: { rate: 0, count: 0 },
})

watch(
  () => props.product,
  (newVal) => {
    Object.assign(
      form,
      newVal || {
        id: 0,
        title: '',
        price: 0,
        category: '',
        image: '',
        rating: { rate: 0, count: 0 },
      },
    )
  },
  { immediate: true },
)

const visible = ref(props.visible)
watch(
  () => props.visible,
  (val) => (visible.value = val),
)

const onSave = () => {
  emit('save', { ...form })
  emit('update:visible', false)
}

const onCancel = () => {
  console.log('Cancel')
  emit('update:visible', false)
}
</script>

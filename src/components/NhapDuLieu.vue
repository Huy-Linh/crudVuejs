<script setup>
import {ref, watch} from 'vue'
const saveEmit = defineEmits()
const props = defineProps({
  productEdit:{
    type: Object,
    default: null
  }
})
const product = ref({
  id: Math.floor(Math.random() * 1000).toString(),
  productName:'',
  os:'',
  cpu:'',
  ram:'',
  storage:'',
  price:'',
})
const osList = ref(['Android','iOS'])
const reset =() =>{
  product.value.id = ''
  product.value.productName = ''
  product.value.os = ''
  product.value.cpu = ''
  product.value.ram = ''
  product.value.storage = ''
  product.value.price = ''
}
const saveButton = () =>{
  saveEmit('save',{...product.value})
  reset()
}
watch(props.productEdit, (newVal) => {
  console.log('new val :',newVal)
  if (newVal) {
    Object.assign(product.value, newVal)
  }
});

</script>
<template>
  {{props.productEdit}}
<v-form @submit.prevent="" @keyup.enter="saveButton">
  <v-text-field
  v-model="product.productName"
  label="Tên sản phẩm">
  </v-text-field>
  <v-select
    v-model="product.os"
    label="Hệ điều hành"
    :items="osList">
  </v-select>
  <v-text-field
    v-model="product.cpu"
    label="CPU">
  </v-text-field>
 <v-text-field
   v-model="product.ram"
   label="RAM">
 </v-text-field>
  <v-text-field
    v-model="product.storage"
    label="Dung lượng">
  </v-text-field>
  <v-text-field
    v-model="product.price"
    label="Giá"
  >
  </v-text-field>
  <v-btn @click="saveButton">Lưu</v-btn>
</v-form>

</template>

<style scoped>

</style>

<script setup>
import {ref, defineEmits, watch,defineProps} from 'vue'
const saveEmit = defineEmits()
const productEdit = defineProps({
  productEdit:{
    type: Object,
    required: true,
  }
})
const product = ref({
  id: null,
  productName:'',
  os:'',
  cpu:'',
  ram:'',
  storage:'',
  price:null,
})
const reset =() =>{
  product.value.id = null
  product.value.productName = ''
  product.value.os = ''
  product.value.cpu = ''
  product.value.ram = ''
  product.value.storage = ''
  product.value.price = null
}
const saveButton = () =>{
  product.value.id = Math.floor(Math.random() * 1000).toString();
  saveEmit('save',{...product.value})
  reset()
}
watch(productEdit.productEdit, (newVal) => {
  if (newVal) {
    Object.assign(product.value, newVal);
  } else {
    reset();
  }
});
</script>
<template>
<form @submit.prevent="">
  <label>
    Tên sản phẩm:
    <input type="text" v-model="product.productName" />
  </label>
  <label>
    Hệ điều hành:
    <select v-model="product.os">
      <option disabled>Chọn hệ điều hành</option>
      <option value="Android">Android</option>
      <option value="iOS">iOS</option>
    </select>
  </label>
  <label>
    CPU:
    <input type="text" v-model="product.cpu">
  </label>
  <label>
    Ram:
    <input type="text" v-model="product.ram">
  </label>
  <label>
    Dung lượng:
    <input type="text" v-model="product.storage">
  </label>
  <label>
    Giá:
    <input type="text" v-model="product.price">
  </label>
  <button @click="saveButton">Lưu</button>
  <button>Hủy</button>
</form>
  {{productEdit}}
</template>

<style scoped>
input, select {
  outline: none;
  width: 200px;
  border: 1px solid #ccc;
  background: none;
  color: rgb(162, 162, 162);
}
form{
  margin: 5px;
  display: flex;
  flex-direction: column;
}
label{
  padding: 3px;
}
button{
  border: 1px solid #ccc;
  width: 100px;
}
</style>

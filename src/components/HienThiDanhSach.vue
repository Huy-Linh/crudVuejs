<script setup>
import NhapDuLieu from "./NhapDuLieu.vue";
import {ref} from 'vue'
const list = ref([
  {
    id: 1,
    productName:"Iphone 16",
    os:'Ios 18',
    cpu:'A18 Pro',
    ram:'8 GB',
    storage:'256 GB',
    price: 123.12
  },
  {
    id: 2,
    productName:"Xiaomi 14T",
    os:'Android 14',
    cpu:'MediaTek Dimensity',
    ram:'12 GB',
    storage:'256 GB',
    price: 123.12
  },
])
const productEdit = ref({
  id: null,
  productName:'',
  os:'',
  cpu:'',
  ram:'',
  storage:'',
  price:null,
})
const addToList = (productSave) => {
  list.value.push(productSave)
}
const deleteButton = (productId) =>{
  list.value.splice(list.value.indexOf(productId),1);
}
const editButton = (product) =>{
  productEdit.value = {...product}
}
</script>
<template>
  <h1>Danh sách sản phẩm điện thoại</h1>
  <button>Thêm mới</button>
  <table>
    <thead>
      <tr>
        <th>Mã sản phẩm</th>
        <th>Tên sản phẩm</th>
        <th>Hệ điều hành</th>
        <th>CPU</th>
        <th>Ram</th>
        <th>Dung lượng</th>
        <th>Giá</th>
        <th>Chức năng</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(value) in list" :key="value.id">
        <td>{{value.id}}</td>
        <td>{{value.productName}}</td>
        <td>{{value.os}}</td>
        <td>{{value.cpu}}</td>
        <td>{{value.ram}}</td>
        <td>{{value.storage}}</td>
        <td>{{value.price}}</td>
        <td>
          <button @click="editButton(value)">Sửa</button>
          <button @click="deleteButton(value.id)">Xóa</button>
        </td>
      </tr>
    </tbody>
  </table>
  <NhapDuLieu @save="addToList" :product-edit="productEdit"></NhapDuLieu>
</template>
<style scoped>
table{
  border: 1px solid black;
  border-collapse: collapse;
}
th, td{
  text-align: center;
  width: 170px;
  border: 1px solid black;
}
button{
  border: 1px solid black;
  margin: 5px;
  padding: 1px;
}
button:active{
  background-color: aqua;
}
</style>

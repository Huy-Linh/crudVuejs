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
  id: '',
  productName:'',
  os:'',
  cpu:'',
  ram:'',
  storage:'',
  price:'',
})
const title = ref("Thêm sản phẩm")
const dialog = ref(false)
const addToList = (productSave) => {
 let index =  list.value.findIndex(product => product.id === productSave.id)
  if(index > -1){
    list.value.splice(index,1,productSave)
  }else {
    list.value.push(productSave)
  }
  dialog.value = false
  return
}
const deleteButton = (productId) =>{
  list.value.splice(list.value.indexOf(productId),1);
}
const editButton = (product) =>{
  console.log(product)
  productEdit.value = {...product}
  dialog.value = true
  title.value = 'Sửa sản phẩm'
}
</script>
<template>
  <v-row justify="center" class="pt-5">
    <h1>Danh sách sản phẩm điện thoại</h1>
  </v-row>
  <v-row justify="center">
    <v-btn @click="dialog = true, title = 'Thêm sản phẩm' ">Thêm mới</v-btn>
  </v-row>
  <v-row>
    <v-table class="w-75 mx-auto border">
      <thead>
      <tr>
        <th class="text-center">Mã sản phẩm</th>
        <th class="text-center">Tên sản phẩm</th>
        <th class="text-center">Hệ điều hành</th>
        <th class="text-center">CPU</th>
        <th class="text-center">Ram</th>
        <th class="text-center">Dung lượng</th>
        <th class="text-center">Giá</th>
        <th class="text-center">Chức năng</th>
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
          <button @click="editButton(value)">  <v-icon icon="mdi-pencil-box"></v-icon></button>
          <button @click="deleteButton(value.id)"><v-icon icon="mdi-delete"></v-icon></button>
        </td>
      </tr>
      </tbody>
    </v-table>
  </v-row>
  <v-dialog v-model="dialog" max-width="500px">
    <v-card>
      <v-card-title>
        <span>{{title}}</span>
      </v-card-title>
      <v-card-text>
        <NhapDuLieu @save="addToList" :productEdit="productEdit"></NhapDuLieu>
      </v-card-text>
    </v-card>
  </v-dialog>

</template>
<style scoped>
v-table{
  border-collapse: collapse;
}
td{
  text-align: center;
  width: 170px;
}
button{
  margin: 5px;
  padding: 1px;
}
button:active{
  background-color: aqua;
}
</style>

<script setup>
import {ref} from 'vue'
const isShow = ref(false)
const name = ref('')
const age = ref()
const hobbies =  ref([])
const sex = ref('')
const city = ref('')
const data = ref([
  {
    name:'Linh',
    age: 22,
    hobbies:(['Đá bóng',]),
    sex: 'Nam',
    city: 'Hải Dương'
  },
  {
    name:'Hà',
    age: 21,
    hobbies:(['Cầu lông',]),
    sex: 'Nam',
    city: 'Hà Nội'
  },
])
function gui(){
  data.value.push({name:name.value, age: age.value, hobbies: [...hobbies.value], sex: sex.value,city: city.value})
  name.value=""
  age.value=""
}
</script>
<template>
  <form @submit.prevent="gui">
    <label for="name">Tên</label>
    <input type="text" name="name" v-model="name">
    <p></p>
    <label for="age">Tuổi</label>
    <input name="age" v-model="age">
    <p></p>
    <input type="checkbox" value="Đá bóng" name="football" v-model="hobbies">
    <label for="football">Đá bóng</label>
    <input type="checkbox" value="Cầu lông" name="badminton" v-model="hobbies">
    <label for="badminton">Cầu lông</label>
    <input type="checkbox" value="Khác" name="other" v-model="hobbies">
    <label for="other">Khác</label>
    <p></p>
    <input type="radio" value="Nam" name="nam" v-model="sex">
    <label for="nam">Nam</label>
    <input type="radio" value="Nữ" name="nu" v-model="sex">
    <label for="nu">Nữ</label>
    <p></p>
    <select v-model="city">
      <option disabled value="">Thành phố</option>
      <option>Hải Dương</option>
      <option>Hà Nội</option>
      <option>Khác</option>
    </select>
    <input type="submit">
  </form>
  <br>
  <table :style="{width:'fit-content'}">
    <thead>
    <tr>
      <th>Tên</th>
      <th>Tuổi</th>
      <th>Sở thích</th>
      <th>Giới tính</th>
      <th>Thành phố</th>
    </tr>
    </thead>
    <tbody >
    <tr v-for="(value, index) in data" :key="index">
      <td >{{value.name}}</td>
      <td>{{value.age}}</td>
      <td>{{value.hobbies}}</td>
      <td>{{value.sex}}</td>
      <td>{{value.city}}</td>
    </tr>
    </tbody>
  </table>
</template>
<style scoped>
th, td {
  border-bottom: 1px solid #ddd;
  text-align: center;
  width: 100px;
}
input, select{
  border: 1px solid #ddd;
}
</style>

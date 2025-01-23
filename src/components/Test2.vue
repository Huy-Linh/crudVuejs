<script setup>
import {ref, watch} from "vue"
const list = ref([
  {
    employeeID: '1',
    firstName: 'Phạm Huy',
    lastName: 'Linh',
    birthDay: '25-02-2003',
    phone: '0944141310',
  },
]);
const employee = ref({
  employeeID: '',
  firstName: '',
  lastName: '',
  birthDay: '',
  phone: '',
});
const empEdit = ref({
  employeeID: '',
  firstName: '',
  lastName: '',
  birthDay: '',
  phone: '',
});
const titleForm = ref('Thêm nhân viên');
const check =  ref({
  isShowForm: false,
  isEditButton: false,
})
const itemsPerPage = 5;

function add() {
  employee.value.employeeID = Math.floor(Math.random() * 1000).toString();
  let ischeckID = list.value.some((e) => e.employeeID === employee.value.employeeID);
  if (!ischeckID) {
    list.value.push({...employee.value});
    reset();
  }
}
function deleteEmp (empID) {
  list.value.splice(list.value.indexOf(empID),1);
}
function editEmp () {
  list.value.splice(list.value.indexOf(empEdit.value),1, {...employee.value});
  check.value.isEditButton = false;
  check.value.isShowForm = false;
  reset()
}
function saveButton(){
  if(check.value.isEditButton === false){
    add()
  }else{
    editEmp()
  }
}
function editButton(emp){
  Object.assign(empEdit.value, emp);
  check.value.isEditButton = true;
  titleForm.value = 'Sửa nhân viên';
  check.value.isShowForm = true;
}
function reset() {
  employee.value.firstName = '';
  employee.value.lastName = '';
  employee.value.birthDay = '';
  employee.value.phone = '';
}
function addNewButton(){
  check.value.isShowForm = true;
  titleForm.value = 'Thêm nhân viên';
}
function cancelButton(){
  check.value.isShowForm = false;
  check.value.isEditButton = false;
  reset()
}

watch(empEdit.value, (newVal) => {
  if (newVal) {
    Object.assign(employee.value, newVal);
  } else {
    reset();
  }
});

</script>
<template>
  <v-container class="pt-2">
   <div>
     <v-row justify="center">
       <h1
       >Danh sách nhân viên</h1>
     </v-row>
   </div>
    <div class="pa-5">
      <v-row justify="center">
        <v-btn v-on:click="addNewButton"
               variant="tonal"
        >Thêm mới</v-btn>
      </v-row>
    </div>
    <div>
      <v-table
        :style="{width: 'fit-content', border: '1px solid #ccc'}" class="mx-auto">
        <thead>
        <tr>
          <th class="text-center">ID</th>
          <th class="text-center">Họ và tên đệm</th>
          <th class="text-center">Tên</th>
          <th class="text-center">Ngày sinh</th>
          <th class="text-center">Số điện thoại</th>
          <th class="text-center">Chức năng</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="employee in list" :key="employee.employeeID">
          <td class="text-center" >{{employee.employeeID}}</td>
          <td class="text-center">{{employee.firstName}}</td>
          <td class="text-center">{{employee.lastName}}</td>
          <td class="text-center">{{employee.birthDay}}</td>
          <td class="text-center">{{employee.phone}}</td>
          <td class="button text-center">
            <v-btn @click="editButton(employee)"
                   variant="fat"
                   class="ma-0"
                   min-width="1px"
            >
              <v-icon icon="mdi-pencil-box"></v-icon>
            </v-btn>
            <v-btn @click="deleteEmp(employee)"
                   variant="fat"
                   class="ma-0"
                   min-width="1px">
              <v-icon icon="mdi-delete"></v-icon>
            </v-btn>
          </td>
        </tr>
        </tbody>
      </v-table>
    </div>
    <div class="pa-5">
        <v-form v-show="check.isShowForm" @submit.prevent="saveButton" class="mx-auto w-66">
          <h3 class="pb-2">{{titleForm}}</h3>
          <v-row>
            <v-col cols="12" xl="6" md="6" sm="6" class="align-center">
              <v-text-field
                v-model="employee.firstName"
                :counter="50"
                placeholder = "Nhập họ và tên đệm"
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12" xl="6" md="6" sm="6">
              <v-text-field

                v-model="employee.lastName"
                :counter="50"
                placeholder = "Nhập tên"
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12" xl="6" md="6" sm="6" class="pt-0">
              <v-text-field
                v-model="employee.birthDay"
                :counter="50"
                placeholder = "Nhập ngày sinh"
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12" xl="6" md="6" sm="6" class="pt-0">
              <v-text-field
                v-model="employee.phone"
                :counter="50"
                placeholder = "Nhập số điện thoại"
                required
              ></v-text-field>
            </v-col>
          </v-row>
          <v-card-action :style="{float: 'right'}" >
            <v-btn
              @click="cancelButton"
              text='Hủy'
              variant="tonal"
            ></v-btn>
            <v-btn
              @click="saveButton"
              text='Lưu'
              variant="tonal"
              class="ml-1"
            ></v-btn>
          </v-card-action>
        </v-form>
    </div>
  </v-container>
</template>

<style scoped>
@media (min-width: 1280px) {
  .v-container {
    max-width: 100%;
  }
}
th, td{
  width: 150px;
}
</style>

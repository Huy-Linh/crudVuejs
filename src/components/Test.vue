<script>
 export default {
   data(){
     return{
       editEmp:{

       },
       employee:{
         employeeID:"",
         firstName:'',
         lastName:'',
         birthDay:'',
         phone:'',
       },
       employeeList:[
         {employeeID:'1', firstName:'Phạm Huy', lastName:'Linh',birthDay:'25/02/2003', phone:'0944141310'},
       ],
       isClickEdit: false,
       isValid: false,
       className:'',
       isShow:false,
       titleHead:'',

     }
   },
   methods: {
     reset(){
       this.employee ={
         employeeID:"",
           firstName:'',
           lastName:'',
           birthDay:'',
           phone:'',
       }
     },
     addEmployee() {
       this.employee.employeeID = Math.floor(Math.random() * 1000)
       let ischeckID = this.employeeList.some(e => e.employeeID === this.employee.employeeID);
         if(!ischeckID){
           this.employeeList.push(this.employee);
           this.isShow=false;
           this.reset()
         }
     },
     deleteEmployee(empId){
       for(let i=0;i<this.employeeList.length;i++){
         if(this.employeeList[i].employeeID==empId){
           this.employeeList.splice(i,1);
         }
       }
     },
     editEmployee(){
       this.employeeList.splice(this.employeeList.indexOf(this.editEmp),1, this.employee);
       this.isClickEdit = false
       this.isShow=false;
       this.reset()
     },
     saveButton(){
       if(this.isClickEdit == false){
         this.addEmployee()
       }else{
         this.editEmployee()
       }
     },
     cancelButton(){
       this.reset()
       this.isShow=false
       this.isClickEdit = false
     },
     editButton(emp){
       this.editEmp=emp
       this.isClickEdit = true
       this.isShow = true
       this.titleHead = 'Edit employee'
     },
     addNewButton(){
       this.isShow=true
       this.titleHead = 'Add new employee'
     },
   },
   watch:{
     editEmp(){
       if(this.editEmp){
         this.employee = Object.assign({},this.editEmp);
       }else{
         this.employee = {}
       }
     }
   },
 }
</script>
<template>
  <div class="container">
    <div>
      <v-row justify="center">
        <h1>Danh sách nhân viên</h1>
      </v-row>
      <v-row justify="end">
        <v-btn v-on:click="addNewButton"
               variant="tonal"
        >Add new employee</v-btn>
      </v-row>
      <v-row>
        <v-table
          :style="{padding: '5px', width: 'fit-content', border: '1px solid #ccc'}" class="mt-2">
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
          <tr v-for="employee in employeeList" :key="employee.employeeID">
            <td >{{employee.employeeID}}</td>
            <td>{{employee.firstName}}</td>
            <td>{{employee.lastName}}</td>
            <td>{{employee.birthDay}}</td>
            <td>{{employee.phone}}</td>
            <td class="button">
              <v-btn @click="editButton(employee)"
                     variant="fat"
                     class="ma-0"
                     min-width="1px"
              >
                <v-icon icon="mdi-pencil-box"></v-icon>
              </v-btn>
              <v-btn @click="deleteEmployee(employee.employeeID)"
                     variant="fat"
                     class="ma-0"
                     min-width="1px">
                <v-icon icon="mdi-delete"></v-icon>
              </v-btn>
            </td>
          </tr>
          </tbody>
        </v-table>
      </v-row>
    </div>
    <v-sheet class="mx-auto" width="790">
      <v-form v-show="isShow">
        <h3 class="py-5">{{titleHead}}</h3>
         <v-row>
           <v-col cols="12" md="6" sm="6"  xs="6">
             <v-text-field
               v-model="employee.firstName"
               :counter="50"
               placeholder = "Nhập họ và tên đệm"
               required
             ></v-text-field>
           </v-col>
           <v-col cols="12" md="6" sm="6"  xs="6">
             <v-text-field
               v-model="employee.lastName"
               :counter="50"
               placeholder = "Nhập tên"
               required
             ></v-text-field>
           </v-col>
           <v-col cols="12" md="6" sm="6"  xs="6">
             <v-text-field
               v-model="employee.birthDay"
               :counter="50"
               placeholder = "Nhập ngày sinh"
               required
             ></v-text-field>
           </v-col>
           <v-col cols="12" md="6" sm="6"  xs="6">
             <v-text-field
               v-model="employee.phone"
               :counter="50"
               placeholder = "Nhập số điện thoại"
               required
             ></v-text-field>
           </v-col>
         </v-row>
        <v-card-action class="pa-0" :style="{float: 'right'}" >
          <v-btn
            @click="cancelButton"
            text='Cancel'
            variant="tonal"
          ></v-btn>
          <v-btn
            @click="saveButton"
            text='Save'
            variant="tonal"
            class="ml-1"
          ></v-btn>
        </v-card-action>
      </v-form>
    </v-sheet>
<!--    Test dialog-->

  </div>
</template>

<style scoped>
.container {
  padding: 10px;
  justify-items: center;
}
@media screen and (min-width: 800px){

}
</style>

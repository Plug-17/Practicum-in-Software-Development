<template>
   <div class="container mt-4"  >  
    <div class="card" style="background-color: bisque;">
        <div class="card-body">
                 <h3 class="text-primary text-center" id="edu" >Education</h3>
        <table class="table table-striped">
             <tr class="fs-5">
                        <th class="text-danger">รหัสวิชา</th>
                        <th class="text-primary">ชื่อวิชา</th>
                        <th class="text-success">หน่วยกิต ({{ totalCredit }} หน่วยกิต) </th>
                        <th class="text-secondary">เกรด</th>
                        <th class="text-info">ปรับเเก้/ลบ</th>
                    </tr>
 
                    <tr v-for="(s,index) in students" :key="index" class="text-success fs-bold fs-4">
 
                    <td>{{ s.id }}</td>
                    <td>{{ s.Subname }}</td>
                    <td> {{ s.credit }}</td>
                    <td>{{ s.grade }}</td>
 
                    <td>
                        <button class="btn btn-warning btn-sm me-2" @click="editData(index)">
                          <i class="bi bi-pen-fill"></i>  เเก้ไข
                        </button>
 
                        <button class="btn btn-danger btn-sm" @click="deleteData(index)">
                            <i class="bi bi-trash-fill"></i>ลบ</button>
                    </td>
                </tr>
        </table>
 
            <div class="text-center">
                 <button class="btn btn-success mb-3 " @click="openForm">เพิ่มข้อมูล</button>
            </div>
       
        <div  v-if="showForm">
            <form @submit.prevent="saveData">
                <table class="table table-bordered text-center w-100">
                    <tr class="fs-5">
                        <th class="text-danger">รหัสวิชา</th>
                        <th class="text-primary">ชื่อวิชา</th>
                        <th class="text-success">หน่วยกิต</th>
                        <th class="text-secondary">เกรด</th>
                        <th  class="text-info">ปรับเเก้/ลบ</th>
                    </tr>
 
                    <tr>
                        <td>
                                <div class="gap-2" style="background-color: bisque;">
                                    <input class="form-control" v-model="form.id" style="background-color: goldenrod;">
                                </div>
                               
                           
                       
                    </td>
 
                     <td>
                        <input class="form-control" v-model="form.Subname" style="background-color: rosybrown;">
                    </td>
 
                     <td>
                       
                                    <div class="gap-2" style="background-color: bisque;">
                                        <select v-model="form.credit" required class="form-select " style="background-color: thistle;">
                                    <option></option>
                                    <option value="1">1</option>
                                    <option value="2">2</option>
                                    <option value="3">3</option>
                                    <option value="4">4</option>
                            </select>
                                    </div>
                               
                                   
                                   
                             
                           
                       
                    </td>
 
                     <td>
                       <select v-model="form.grade" required class="form-select" style="background-color: khaki;">
                                    <option></option>
                                    <option value="A">A</option>
                                    <option value="B+">B+</option>
                                    <option value="B">B</option>
                                    <option value="C+">C+</option>
                                    <option value="C">C</option>
                                    <option value="D+">D+</option>
                                    <option value="D">D</option>
                                    <option value="F">F</option>
                            </select>
                    </td>
 
                    <td>
                       
                           <button type="submit" class="btn btn-success btn-sm me-2">
                                บันทึก
                        </button>
                       
                       
 
                        <button type="button" class="btn btn-secondary btn-sm" @click="cancelEdit" style="background-color: beige;">
                            ยกเลิก
                        </button>
                    </td>
                </tr>
                   
 
                </table>
            </form>
        </div>
        </div>
    </div>
       
   </div>
</template>
 
<script setup>
import { ref,onMounted,computed } from 'vue';

 
 
const students = ref([])
const editIndex = ref(-1)
const showForm = ref(false)
 

onMounted(async() => {
    const res = await fetch("http://localhost:3001/students")
    students.value = await res.json()
})
const form = ref({
    id:"",
    Subname:"",
    credit:"",
    grade:""
})
 
function openForm(){
    showForm.value =! showForm.value
 
    if(showForm.value) {
         editIndex.value = -1
 
    form.value={
        id:"",
        Subname:"",
        credit:"",
        grade:""
    }
    }
   
}
 
async function saveData(){

  if(editIndex.value === -1){

    const res = await fetch("http://localhost:3001/students",{
      method:"POST",
      headers:{
        "Content-Type":"application/json"
      },
      body: JSON.stringify({
        Subname: form.value.Subname,
        credit: form.value.credit,
        grade: form.value.grade,
        id: form.value.id
      })
    })

    const newData = await res.json()
    students.value.push(newData)

  }else{

    const id = students.value[editIndex.value].id

    const res = await fetch(`http://localhost:3001/students/${id}`,{
      method:"PUT",
      headers:{
        "Content-Type":"application/json"
      },
      body: JSON.stringify({
        id:id,
        Subname: form.value.Subname,
        credit: form.value.credit,
        grade: form.value.grade
      })
    })

    const updated = await res.json()
    students.value[editIndex.value] = updated
  }

  showForm.value = false
}

   

   
    
   

 
const totalCredit = computed(() => {
  if(!students.value.length) return 0
  return students.value.reduce((sum, s) => sum + parseInt(s.credit || 0), 0)
})

function editData(index) {
    showForm.value  = true
    editIndex.value  = index
    form.value = {...students.value[index]}
}
 
function cancelEdit(){
    showForm.value = false
}
 
async function deleteData(index){

  const id = students.value[index].id

  await fetch(`http://localhost:3001/students/${id}`,{
    method:"DELETE"
  })

  students.value.splice(index,1)
}
 
</script>
 
<style lang="scss" scoped>
 
</style>

<template>

  <project1></project1>

  <section class="py-5 color" id="home">
    <div class="container" style="margin-top:120px;" id="go">
      <div class="row align-items-center">

        <div class="col-md-7">

          <h1 class="text-primary mt-5">WELCOME TO</h1>
          <h1 class="text-primary">PORTFOLIO</h1>

          <div class="fs-4">
            <h3 class="text-primary">ชื่อ: {{ name }}</h3>
            <p class="text-danger">รหัสนิสิต: {{ subAll.passnisit }}</p>
            <p class="text-info">คณะ: {{ subAll.faculty }}</p>
            <p class="text-muted">สาขาวิชา: {{ subAll.majorName }}</p>
            <p class="text-success">รหัสสาขา: {{ subAll.major }}</p>
            <p class="text-secondary">โรงเรียน: {{ subAll.Hihgschool }}</p>

            <button class="btn btn-primary" @click="EditData()">แก้ไขรายละเอียด</button>
          </div>

          
          <div class="card mt-4" v-if="isEditing" style="margin-right:150px;background-color:navajowhite;">
            <div class="card-body">

              <form @submit.prevent="saveData">

                  <div class="mb-2 fs-4" >
              <label>ชื่อ</label>
              <input  class="form-control" v-model="editFrom.name" style="background-color: darkkhaki">
            </div>

             <div class="mb-2 fs-4">
              <label>รหัสนิสิต</label>
              <input  class="form-control" v-model="editFrom.passnisit" style="background-color: peru">
            </div>

             <div class="mb-2 fs-4">
              <label>คณะ</label>
              <input  class="form-control" v-model="editFrom.faculty" style="background-color: forestgreen;">
            </div>

             <div class="mb-2 fs-4">
              <label>สาขาวิชา</label>
              <input  class="form-control" v-model="editFrom.majorName" style="background-color: aqua;">
            </div>

             <div class="mb-2 fs-4">
              <label>รหัสสาขา</label>
              <input  class="form-control" v-model="editFrom.major" style="background-color: sandybrown;">
            </div>

             <div class="mb-3 fs-4">
              <label>โรงเรียน</label>
              <input  class="form-control" v-model="editFrom.Hihgschool"  style="background-color: gold;">
            </div>

                <button class="btn btn-success btn-sm me-2" type="submit">บันทึก</button>
                <button class="btn btn-primary btn-sm me-2" type="button" @click="cancelEdit()">ยกเลิก</button>

              </form>

            </div>
          </div>

        </div>

        
        <div class="col-md-5 text-center">
          <img src="./component/photo/photomy.jpg"
               class="img-fluid"
               style="height:500px;">
        </div>

      </div>

      <div class="py-5 mt-5 d-flex justify-content-center">
        <project2></project2>
      </div>

      <div class="py-5 mt-5 d-flex justify-content-center">
        <project3></project3>
      </div>

    </div>
  </section>

</template>
<script setup>

import project1 from './component/project1.vue';
import project2 from './component/project2.vue';
import project3 from './component/project3.vue';
import fishData from "./data/fish.json"

import { ref, onMounted } from 'vue'
let fish = ref([])

let name = ref("ชินวัตร กลิ่นนาค")

let subAll = ref({
  passnisit: "6730200464",
  faculty: "วิทยาศาสตร์ ศรีราชา",
  majorName: "วิทยาการคอมพิวเตอร์",
  major: "S05",
  Hihgschool: "โรงเรียนมารีวิทย์บ่อวิน"
})




onMounted(async () => {
  const res = await fetch("http://localhost:3000/profile")
  const data = await res.json()

  name.value = data.name

  subAll.value = {
    passnisit: data.passnisit,
    faculty: data.faculty,
    majorName: data.majorName,
    major: data.major,
    Hihgschool: data.Hihgschool
  }
  fish.value = fishData.fish
})


async function saveData(){

  const newData = {
    name: editFrom.value.name,
    passnisit: editFrom.value.passnisit,
    faculty: editFrom.value.faculty,
    majorName: editFrom.value.majorName,
    major: editFrom.value.major,
    Hihgschool: editFrom.value.Hihgschool
  }

  await fetch("http://localhost:3000/profile", {
    method: "PUT",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify(newData)
  })

  name.value = newData.name
  subAll.value = newData

  isEditing.value = false
}

let isEditing = ref(false)

let editFrom =  ref({})


async function EditData(){

  if(isEditing.value){
    isEditing.value = false
    return
  }

  const res = await fetch("http://localhost:3000/profile")
  const data = await res.json()

    editFrom.value = {
    name: data.name,
    passnisit: data.passnisit,
    faculty: data.faculty,
    majorName: data.majorName,
    major: data.major,
    Hihgschool: data.Hihgschool
  }

  isEditing.value = true
}


function cancelEdit(){
    isEditing.value = false
}








</script>

<style lang="scss">
#home {
  scroll-margin-top: 100px;
}

.color {
  background-color: rgb(230, 194, 147);
  min-height: 100vh;
  width: 1400px;
}

body{
  margin:0;
  background-color: rgb(230, 194, 147);
}





</style>


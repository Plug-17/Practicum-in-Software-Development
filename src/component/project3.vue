<template>
    <!---photo-->
<section id="photo" style="background-color: rgb(230, 194, 147);">
  <div class="container" >
    <h3 class="text-center text-primary my-3 pt-5">Photo For Me</h3>

    <!-- row -->
    <div class="row justify-content-center align-items-center mt-5">

      <!-- card 1 -->
      <div class="col-lg-3 col-md-6 col-sm-12">
        <div class="card h-100">
        
                <img src="D:\project\src\component\photo\photo1.jpg" class="w-200" style="height:300px; object-fit:cover;" >
          
        
          <div class="card-body" style="background-color: aquamarine;">
            <h5 class="card-title text-center">พระพิรุณ</h5>
            <p class="card-text" v-if="show1">
              เป็นสิ่งเด็กเกษตรทุกคนนับถือบูชา เเละถือเป็นสัญลักษณ์ของมหาลัย โดยส่วนตัวผมได้ไปกราบขอพรไห้ติด Computer Science ซึ่งสมหวังดั่งที่ขอไว้
            </p>
            <div class="text-end">
              <a href="#" class="btn btn-sm btn-danger" @click.prevent="show1=!show1">
               <i class="bi bi-bookmark"></i> เปิด/ปิด
              </a>
            </div>
          </div>
        </div>
      </div>

      <!-- card 2 -->
      <div class="col-lg-3 col-md-6 col-sm-12">
        <div class="card h-100">
          <img src="D:\project\src\component\photo\photo2.jpg" alt="" class="w-200" style="height:300px; object-fit:cover;">
          <div class="card-body"  style="background-color: palegreen">
            <h5 class="card-title text-center">เเมวบ้านญาติ</h5>
            <p class="card-text" v-if="show2">ไปบ้านญาติช่วงเดือนกุมภาพันธ์ โดยพบเจอเเมวตังนั้นจึงถ่ายรูปกลับมาเพราะเห็นมันน่ารักดี</p>
            <div class="text-end">
              <a href="#" class="btn btn-sm btn-success" @click.prevent="show2=!show2">
               <i class="bi bi-bookmark"></i> เปิด/ปิด
              </a>
            </div>
          </div>
        </div>
      </div>

      <!-- card 3 -->
      <div class="col-lg-3 col-md-6 col-sm-12">
        <div class="card h-100">
          <img src="D:\project\src\component\photo\photo3.jpg" alt="" class="w-200" style="height:300px; object-fit:cover;">
          <div class="card-body" style="background-color: salmon;">
            <h5 class="card-title text-center"> งานศิลปะวิชา pigment art</h5>
            <p class="card-text" v-if="show3">เป็นช่วงที่อาจารย์ไห้ถ่ายรูปโดยไห้เลียนเเบบรูปภาพใดก็ได้ กลุ่มผมจึงได้เอารูปคนเล่นไผ่มาเป้นเเรงบัลดาลใจในการส่งงาน</p>
            <div class="text-end">
              <a href="#" class="btn btn-sm btn-info" @click.prevent="show3=!show3">
                <i class="bi bi-bookmark"></i> เปิด/ปิด
              </a>
            </div>
          </div>
        </div>
      </div>

      <!-- card 4 -->
      <div class="col-lg-3 col-md-6 col-sm-12">
        <div class="card h-100">
          <img src="D:\project\src\component\photo\photo4.jpg" alt="" class="w-200" style="height:300px; object-fit:cover;">
          <div class="card-body" style="background-color: khaki;">
            <h5 class="card-title text-center">เกาะลอยศรีราชา</h5>
            <p class="card-text" v-if="show4">ผมไปเที่ยวกับครอบครัว เเล้วเห็นบรรยากาศตรงนี้สวยพอดี เลยถ่ายรูปเอาไว้</p>
            <div class="text-end">
              <a href="#" class="btn btn-sm btn-warning" @click.prevent="show4=!show4">
                <i class="bi bi-bookmark"></i> เปิด/ปิด
              </a>
            </div>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>
</template>

<script setup>
import { ref } from 'vue';

const show1 =  ref(true)
const show2 =  ref(true)
const show3 =  ref(true)
const show4 =  ref(true)
</script>

<style lang="scss" scoped>

</style>
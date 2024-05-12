<template>
  <div>
    <h1 class="text-xl font-bold footer-center">เพิ่มข้อมูลผู้ใช้</h1>
    <br />
    <div class="footer-center">
        <div class="form-control">
          <label class="input input-bordered flex items-center gap-2">
            Email
            <input type="email" class="grow" placeholder="daisy@site.com" v-model="add.email" />
          </label>
        </div>
        <br />
        <div class="form-control">
          <label class="input input-bordered flex items-center gap-2">
            Password
            <input type="password" class="grow" placeholder="***********" v-model="add.password"/>
          </label>
        </div>
        <br />
        <div class="form-control">
          <label class="input input-bordered flex items-center gap-2">
            ConfirmPassword
            <input type="password" class="grow" placeholder="***********" v-model="add.confirm_password"/>
          </label>
        </div>
        <br>
        <button class="btn btn-success" @click="check">เพิ่มข้อมูล</button>
    </div>
  </div>
</template>
<script setup>
  import { ref } from 'vue'
  import axios from 'axios'
  import routes from '../router';

  const add = ref ({
    email : '',
    password : '',
    confirm_password : ''
  })

  const insert_user = async () => {
    await axios.post(`${import.meta.env.VITE_API}/users`,{
      "email" : add.value.email,
      "password" : add.value.confirm_password
    })
    .then((response) => {
      console.log(response)
    }).catch((err) => {
      console.log(err)
    })
  }

  const check = async () => {
    if(add.value.password == add.value.confirm_password) {
      await insert_user()
      await alert("เพิ่มข้อมูลสำเร็จ")
      await routes.push('/')
    } else {
      alert("รหัสผ่านไม่ถูกต้อง")
      add.value=''
    }
  }
</script>
<style lang="scss" scoped></style>

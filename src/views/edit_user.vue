<template>
  <div>
    <h1 class="text-xl font-bold footer-center">แก้ไขข้อมูลผู้ใช้</h1>
    <br />
    <div class="footer-center">
        <div class="form-control">
          <label class="input input-bordered flex items-center gap-2">
            Email
            <input type="email" class="grow" placeholder="daisy@site.com" v-model="user.email" />
          </label>
        </div>
        <br />
        <div class="form-control">
          <label class="input input-bordered flex items-center gap-2">
            Password
            <input type="password" class="grow" placeholder="***********" v-model="user.password"/>
          </label>
        </div>
        <br />
        <div class="form-control">
          <label class="input input-bordered flex items-center gap-2">
            ConfirmPassword
            <input type="password" class="grow" placeholder="***********" v-model="user.confirm_password"/>
          </label>
        </div>
        <br>
        <button class="btn btn-success" @click="check">เพิ่มข้อมูล</button>
    </div>
  </div>
</template>
<script setup>
  import { ref, onMounted } from 'vue'
  import axios from 'axios'
  import {useRoute} from 'vue-router';
import router from '../router';

  const route = useRoute()
  const user = ref ({
    email : '',
    password : '',
  })

  const fetch_single_user = async () => {
    await axios.get(`${import.meta.env.VITE_API}/users/${route.params.id}`)
    .then((response) => {
      user.value.email = response.data.data[0].email
    }).catch((err) => {
      console.log(err)
    })
  }

  onMounted(() => fetch_single_user())

  const edit_user = async () => {
    await axios.put(`${import.meta.env.VITE_API}/users/${route.params.id}`,{
      "email" : user.value.email,
      "password" : user.value.confirm_password
    }).then((response) => {
      console.log(response)
    }).catch((err) => {
      console.log(err)
    })
  }

  const check = async () => {
    if(user.value.password !== user.value.confirm_password) {
     await alert("รหัสผ่านไม่ถูกต้อง")
     user.value.password = ''
     user.value.confirm_password = ''
    } else {
      await edit_user()
      await alert("แก้ไขข้อมูลสำเร็จ")
      await router.push('/')
    }
  }
</script>
<style lang="scss" scoped></style>

<template>
  <router-link to="/add">
  <button class="btn btn-accent">เพิ่มผู้ใช้งาน</button>
  </router-link>
    <div class="overflow-x-auto">
  <table class="table">
    <!-- head -->
    <thead>
      <tr>
        <th></th>
        <th>Email</th>
        <th>Role</th>
        <th>Tool</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(user, index) in users">
        <th>{{ index+1}}</th>
        <td>{{ user.email }}</td>
        <td>{{ user.role }}</td>
        <td>
          <router-link :to="`/edit/${user.id}`">
            <button class="btn btn-secondary mx-2">แก้ไข</button>
          </router-link>
          <button class="btn btn-primary" @click="delete_users(user.id)">ลบ</button>
        </td>
      </tr>
    </tbody>
  </table>
</div>
  </template>
  <script setup>
  import { ref, onMounted } from 'vue'
  import axios from 'axios'

  const users = ref({})

  const fetch_users = async () => {
    await axios.get(`${import.meta.env.VITE_API}/users`)
    .then((response) => {
      users.value = response.data.data
    }).catch((err) => {
      console.log(err)
    })
  }

  const delete_users = async (id) => {
    await axios.delete(`${import.meta.env.VITE_API}/users/${id}`)
    .then((response) => {
      console.log(response)
      fetch_users()
    }).catch((err) => {
      console.log(err)
    })
  }

  onMounted(() => fetch_users())
  </script>
  <style lang="scss" scoped>
    
  </style>
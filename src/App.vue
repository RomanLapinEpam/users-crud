<template>
  <div id="app">
    <create-user-dialog ref='userForm' @create='createUser' @update='updateUser'/>
    <users-table :users='users' @remove='removeUser' @edit='openEditForm'/>
  </div>
</template>

<script>
import Vue from 'vue'
import VueMaterial from 'vue-material'
import 'vue-material/dist/vue-material.min.css'
import 'vue-material/dist/theme/default-dark.css'

import UsersTable from './components/UsersTable'
import CreateUserDialog from './components/CreateUserDialog'

import { defaultUsers } from './const/defaultData'

Vue.use(VueMaterial)

export default {
  name: 'App',
  components: {
    UsersTable,
    CreateUserDialog
  },
  data () {
    return {
      users: []
    }
  },
  created: function () {
    const storageUsers = JSON.parse(localStorage.getItem('crudUsers'))
    const users = storageUsers || defaultUsers
    this.users.push(...users)
  },
  methods: {
    createUser (user) {
      const { users } = this
      const id = Math.max.apply(Math, users.map(user => user.id)) + 1

      this.users.push({
        ...user,
        id
      })
    },
    updateUser (user) {
      const userIndex = this.users.map(user => user.id).indexOf(user.id)
      this.users.splice(userIndex, 1, user)
    },
    openEditForm (id) {
      const userForm = this.$refs.userForm
      const user = this.users.filter(user => user.id === id)[0]
      userForm && userForm.editUser(user)
    },
    removeUser (id) {
      this.users = this.users.filter(user => user.id !== id)
    }
  },
  watch: {
    users: {
      handler: function (newUsers) {
        localStorage.setItem('crudUsers', JSON.stringify(newUsers))
      },
      deep: true
    }
  }
}
</script>

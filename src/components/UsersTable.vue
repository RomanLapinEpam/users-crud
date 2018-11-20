<template>
  <div >
     <md-table v-model="users" md-card>
      <md-table-row slot="md-table-row" slot-scope="{ item }">
        <md-table-cell md-label="ID" md-numeric>{{ item.id }}</md-table-cell>
        <md-table-cell md-label="Name">{{ item.name }}</md-table-cell>
        <md-table-cell md-label="Email">
          <a :href="`mailto:${item.mail}`">{{ item.email }}</a>
        </md-table-cell>
        <md-table-cell md-label="Gender">
          <span v-if="item.gender">
            {{ item.gender === "M" ? "Male" : "Female" }}
          </span>
        </md-table-cell>
        <md-table-cell md-label="Job">{{ item.job }}</md-table-cell>
        <md-table-cell>
          <md-button @click="editUser(item.id)" class="md-raised">Edit</md-button>
          <md-button @click="removeUser(item.id)" class="md-raised md-accent">Remove</md-button>
        </md-table-cell>
      </md-table-row>
    </md-table>
  </div>
</template>

<script>
export default {
  name: 'UsersTable',
  props: {
    users: {
      type: Array,
      default: function () {
        return []
      }
    }
  },
  methods: {
    removeUser (id) {
      this.$emit('remove', id)
    },
    editUser (id) {
      this.$emit('edit', id)
    }
  }
}
</script>

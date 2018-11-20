 <template>
  <div>
    <md-dialog :md-active.sync="showDialog">
      <form novalidate class="md-layout">
        <md-card class="md-layout-item md-small-size-100">
          <md-card-header>
            <div class="md-title">Create user</div>
          </md-card-header>

          <md-card-content>
            <div class="md-layout md-gutter">
              <div class="md-layout-item md-small-size-100">
                <md-field >
                  <label for="name">Name</label>
                  <md-input name="name" id="name"  v-model="form.name"/>
                </md-field>
              </div>
            </div>

            <div class="md-layout md-gutter">
              <div class="md-layout-item md-small-size-100">
                <md-field >
                  <label for="gender">Gender</label>
                  <md-select name="gender" id="gender" v-model="form.gender">
                    <md-option></md-option>
                    <md-option value="M">Male</md-option>
                    <md-option value="F">Female</md-option>
                  </md-select>
                </md-field>
              </div>
            </div>

            <div class="md-layout md-gutter">
              <div class="md-layout-item md-small-size-100">
                <md-field >
                  <label for="job">Job</label>
                  <md-input name="job" id="job" v-model="form.job"/>
                </md-field>
              </div>
            </div>

            <div class="md-layout md-gutter">
              <div class="md-layout-item md-small-size-100">
                <md-field >
                  <label for="email">Email</label>
                  <md-input name="email" id="email" v-model="form.email"/>
                </md-field>
              </div>
            </div>

            <md-dialog-actions>
              <md-button class="md-accent md-raised" @click="closeForm">Cancel</md-button>
              <md-button class="md-primary md-raised" @click="saveForm">Save</md-button>
            </md-dialog-actions>
          </md-card-content>
        </md-card>
      </form>
    </md-dialog>

    <md-button class="md-primary md-raised" @click="showDialog = true">Create user</md-button>
  </div>
</template>

<script>
const emptyForm = {
  id: null,
  name: '',
  gender: '',
  job: '',
  email: ''
}

export default {
  name: 'CreateUserDialog',
  data: () => ({
    form: { ...emptyForm },
    showDialog: false
  }),
  methods: {
    saveForm () {
      if (this.form.id) {
        this.$emit('update', this.form)
      } else {
        this.$emit('create', this.form)
      }

      this.closeForm()
    },
    editUser (user) {
      this.form = {...user}
      this.showDialog = true
    },
    closeForm () {
      this.showDialog = false
      this.form = { ...emptyForm }
    }
  }
}
</script>

<style scoped>
.md-dialog {
  max-width: 768px;
}
</style>

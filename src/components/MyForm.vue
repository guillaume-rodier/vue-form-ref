<template>
  <form
    id="app"
    class="my-form-class"
    @submit="checkForm"
  >
    <p v-if="errors.length > 0" class="error-container">
      <b>Please correct the following error(s):</b>
      <ul>
        <li v-for="(error, index) in errors" :key="index" class="error-text">
          {{ error }}
        </li>
      </ul>
    </p>

    <div class="input-container">
      <label for="firstname" class="label-style">Firstname</label>
      <input v-model="user.firstname" id="firstname" />
    </div>

    <div class="input-container">
      <label for="lastname" class="label-style">Lastname</label>
      <input v-model="user.lastname" id="lastname" />
    </div>
  </form>
</template>

<script>
export default {
  name: "MyForm",

  data() {
    return {
      errors: [],
      user: {
        firstname: null,
        lastname: null,
      },
    };
  },

  methods: {
    checkForm() {
      this.errors = [];

      if (this.user.firstname && this.user.lastname) {
        return this.user;
      }

      if (!this.user.firstname || this.user.firstname === "") {
        this.errors.push('Firstname required.');
      }

      if (!this.user.lastname || this.user.lastname === "") {
        this.errors.push('Lastname required.');
      }
    }
  },

  watch: {
    "user.firstname"() {
      if (this.user.firstname === "") {
        this.user.firstname = null;
      }
    },

    "user.lastname"() {
      if (this.user.lasname === "") {
        this.user.lasname = null;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.my-form-class {
  .error-container {
    .error-text {
      color: red;
      font-weight: bold;
    }
  }

  .input-container {
    margin: 10px;

    .label-style {
      margin-right: 10px;
    }
  }
}
</style>

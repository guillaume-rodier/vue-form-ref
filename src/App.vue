<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <div>
      <MyForm ref="MyForm" />
      <button @click="submitData">Submit</button>
    </div>
    <div v-if="conditionDataUser">
      Well done, your user is named {{ user.firstname }} {{ user.lastname }}
    </div>
  </div>
</template>

<script>
import MyForm from './components/MyForm.vue';

export default {
  name: 'App',

  components: {
    MyForm,
  },

  computed: {
    conditionDataUser() {
      if (
        this.user !== null &&
        (this.user?.firstname !== null && this.user?.firstname !== undefined && this.user?.firstname !== "") &&
        (this.user?.lastname !== null && this.user?.lastname !== undefined && this.user?.lastname !== "")
      ) {
        return true;
      } else {
        return false;
      }
    },
  },

  data() {
    return {
      user: null,
    };
  },

  methods: {
    submitData() {
      let data = this.$refs.MyForm.checkForm();

      if (data !== undefined) {
        this.user = data;
      } else {
        this.user = null;
      }
    },
  },

  // You can see, when you click on submit button with good data, and change input value after, the data in "user" parent change too !
  watch: {
    "user.firstname"() {
      console.log("user.firstname ici:", this.user.firstname)
    },

    "user.lastname"() {
      console.log("user.lastname ici:", this.user.lastname)
    },
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input
        type="text"
        placeholder="enter the name you search"
        v-model="keyWord"
      />&nbsp;
      <button @click="getUsersData">Search</button>
    </div>
  </section>
</template>

<script>
import axios from 'axios'
export default {
  name: 'SearchComponents',
  data() {
    return {
      keyWord: '',
      arrayData: []
    }
  },
  methods: {
    getUsersData() {
      this.$bus.$emit('usersData', {
        isFirst: false,
        isLoading: true,
        errMsg: '',
        user: []
      })
      axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
        (response) => {
          if (response.data.items.length === 0) {
            this.$bus.$emit('usersData', {
              errMsg: `Cannot find user ${this.keyWord}`,
              isLoading: false
            })
          } else {
            this.$bus.$emit('usersData', {
              isLoading: false,
              errMsg: '',
              user: response.data.items
            })
          }
        },
        (error) => {
          this.$bus.$emit('usersData', {
            isLoading: false,
            errMsg: error.message,
            user: []
          })
        }
      )
    }
  }
}
</script>

<style></style>

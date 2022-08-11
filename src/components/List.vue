<template>
  <div class="row">
    <div v-for="userList in info.user" :key="info.user.login" class="card">
      <a :href="userList.html_url" target="_blank">
        <img :src="userList.avatar_url" style="width: 100px" />
      </a>
      <p class="card-text">{{ info.user.login }}</p>
    </div>
    <h1 v-show="info.isFirst">Welcome to search</h1>
    <h1 v-show="info.isLoading">Loading........</h1>
    <h1 v-show="info.errMsg">{{ info.errMsg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'ListComponents',
  data() {
    return {
      info: {
        isFirst: true,
        isLoading: false,
        errMsg: '',
        user: []
      }
    }
  },
  mounted() {
    this.$bus.$on('usersData', (data) => {
      this.info = { ...this.info, ...data }
    })
  }
}
</script>

<style scoped>
.album {
  min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;
  padding-bottom: 3rem;
  background-color: #f7f7f7;
}
.card {
  float: left;
  width: 33.333%;
  padding: 0.75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}
.card > img {
  margin-bottom: 0.75rem;
  border-radius: 100px;
}
.card-text {
  font-size: 85%;
}
</style>

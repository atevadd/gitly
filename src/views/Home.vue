<template>
  <div class="home">
    <h1>Find a user on github</h1>
    <Input
      label="Find a user on github"
      InputType="search"
      @search="findUser($event)"
    />

    <div class="search-result" v-if="result">
      <ResultCard :name="user.login" :imgUrl="user.avatar_url" v-for="user in result" :key="user.id" />
    </div>
    <div class="empty-state" v-else-if="error === 'Failed to fetch' " >
      <i class='bx bx-wifi-off' ></i>
      <p>It appears that you do not have internet connection</p>
    </div>
    <div class="empty-state" v-else>
      <i class="bx bx-search-alt"></i>
      <p>You haven't search for anything, type in the input field to begin</p>
    </div>
  </div>
</template>

<script>
import Input from "@/components/Input.vue";
import ResultCard from "@/components/ResultCard.vue";

export default {
  name: "Home",
  components: {
    Input,
    ResultCard,
  },
  emits:['search'],
  data() {
    return {
      result: null,
      clientId:'0ed705e5815fa23fa13b',
      clientSecret: '95eb90d8af643bd97c02dc881c2c38e5e91adb65',
      error: null
    };
  },
  methods: {
    search() {
      // this.$emit('search')
      console.log("Printed value");
    },
    findUser(value) {
    
      let response;

      // const profileResponse = fetch(`https://api.github.com/users/${value}?client_id=${this.clientId}&client_secret=${this.clientSecret}`)
      const profileResponse = fetch(`https://api.github.com/search/users?q=${value}&page=1`)
      .then(res => res.json())
      .then(data => {
        response = data.items
        this.result = response;
        // console.log(response);
      })
      .catch(err => {
        console.log(err.message)
        this.error = err.message
        console.log(this.error)
      })
    },
  },
};
</script>

<style lang="scss" scoped>
.home {
  margin: 15px 0;

  h1 {
    font-weight: 600;
    text-align: center;

    @media screen and (max-width: 480px) {
      font-size: 1.5rem;
    }
  }

  .search-result {
    width: 95%;
    margin: 40px auto 20px;
    display: grid;
    grid-template-columns: repeat(5, minmax(0, 1fr));
    gap: 25px;
    
    @media screen and (max-width: 480px) {
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 15px;
    }
    @media screen and (min-width: 481px) and (max-width: 768px) {
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 15px;
    }
  }
  .empty-state, .error-state {
    width: 30%;
    margin: 60px auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    @media screen and (max-width: 480px) {
      width: 80%;
    }

    i {
      display: flex;
      font-size: 4rem;
    }
    p {
      text-align: center;
    }
  }
}
</style>

<template>
<header>
  <h1 class="brand-name">Github Finder</h1>

  <nav>
    <router-link :to="{name: 'Home'}">Home</router-link>
    <router-link :to="{name: 'About'}">About</router-link>
    <!-- <router-link :to="{ name: 'User', params: {id: id}}">User</router-link> -->
  </nav>
</header>
  <main>
    <router-view @search="results"/>
  </main>
</template>


<script>
export default {
  name: "App",
  data(){
    return{
      id: 4,
      result: "Nothing yet"
    }
  },
  methods: {
    results(){
      console.log(this.result)
    }
  }
}
</script>

<style lang="scss">

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "poppins", sans-serif;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
body{
  overflow-x: hidden;
}
header{
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 15px;
  background-color: #2c3e50;

  h1{
    color: #fff;

    @media screen and (max-width: 480px) {
     font-size: 1.5rem;
    }
  }

  nav{
    a{
      color: #42b983;
      text-decoration: none;
      display: inline-block;
      margin-left: 20px;
      transition: .25s ease;

      &:hover{
        text-decoration: underline;
      }
    }
  }
}

main{
  position: relative;
  // border: 4px solid red;
}
</style>

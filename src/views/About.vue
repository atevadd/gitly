<template>
  <div class="about">
    <i class='bx bx-user-circle' ></i>
    <h1>This is Github finder was built by Tofunmi Adeniyi using Vue, Vue-router, SCSS and Github API.</h1>
  </div>
</template>

<script>
export default {
  name: "About"
}
</script>

<style lang="scss" scoped>
.about{
  width: 100%;
  height: 80vh;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;

  i{
    font-size: 4rem;
    color: #333;
  }
  
  h1{
    text-align: center;
    font-weight: 600;
    color: #333;
  }
}
</style>

<template>
  <div class="search-card">
    <img :src="imgUrl" alt="" />
    <div class="card-text">
      <h2>{{ name }}</h2>
      <router-link :to="{ name: 'UserProfile', params: { userName: name } }"
        >view profile</router-link
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "ResultCard",
  props: {
    imgUrl: String,
    name: {
      type: String,
      required: true,
      default: "John Doe",
    },
    userId: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      id: 4,
    };
  },
};
</script>

<style lang="scss" scoped>
.search-card {
  width: 100%;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 0 3px 13px rgba($color: #000000, $alpha: 0.2);
  border: 1px solid #aaa;

  img {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: inline-block;
    margin-right: 10px;
  }

  .card-text {
    position: relative;

    h2 {
      font-size: 1.2rem;
      color: #2c3e50;
      font-weight: 600;
      // margin-bottom: ;
      // border: 1px solid;
      width: 14ch;
      line-height: 1.2;
      overflow: hidden;
      white-space: nowrap;
      word-wrap: normal;
      text-overflow: ellipsis;

      @media screen and (max-width: 480px) {
        width: 10ch;
      }
    }
    a {
      display: inline-block;
      text-decoration: none;
      color: #42b983;
      font-weight: 400;
      font-size: 0.88rem;
      // border: 1px solid;
      line-height: 1.2;

      &:hover {
        text-decoration: underline;
      }
    }
  }
}
</style>
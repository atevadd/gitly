<template>
  <div class="input-box">
    <!-- <label :for="label">{{ label }}</label> -->
    <input :type="type" v-model="value" @keyup="startSearch(value)" :id="label">
    <button @click="search(value)"><i class="bx bx-search"></i></button>
  </div>
</template>

<script>
export default {
  name:"Input",
  props:{
    label:{
      type: String,
      default: "Name"
    },
    type: String
  },
  data(){
    return{
      value: null,
    }
  },
  methods: {
    search(value){
      this.$emit('search', value)
    },
    startSearch(value){
      this.$emit('search-value', value)
    }
  }
}
</script>

<style lang="scss" scoped>
.input-box{
  width: 50%;
  margin: 15px auto;
  position: relative;

  @media screen and (max-width: 480px){
    width: 85%;
  }

  input{
    display: block;
    height: 50px;
    border-radius: 50px;
    width: 100%;
    outline: none;
    border: 1px solid #aaa;
    padding: 0 20px;


    &:focus{
      border: 2px solid #42b983;
    }
  }
  button{
    position: absolute;
    top: 50%;
    right: 5px;
    transform: translateY(-50%);
    background-color: #2c3e50;
    color: #fff;
    border-radius: 50%;
    border: none;
    outline: none;
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: .25s ease;

    &:hover{
      background-color: darken($color: #2c3e50, $amount: 10%);
    }

    i{
      font-size: 1.3rem;
    }
  }
}
</style>
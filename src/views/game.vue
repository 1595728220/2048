<template>
  <div class="pan">
    <div v-for="(arr,ind) of num" :key="ind">
      <my-square :num="value" v-for="(value,index) of arr" :key="index"></my-square>
    </div>
  </div>
</template>
<script>
import Square from "../components/square";
export default {
  data() {
    return {
      num:[[0,0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0]]
    };
  },
  components: {
    "my-square": Square
  }
};
</script>
<style lang="scss" scoped>
    .pan{
        width:500px;
        height:500px;
        border-radius: 10px;
        background:#BBADA0;
        position: absolute;
        top:50%;
        left:50%;
        transform: translate(-50%,-50%)
    }
</style>

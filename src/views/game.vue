<template>
  <div class="pan">
      <my-square :num="num"></my-square>
  </div>
</template>
<script>
import Square from "../components/square";
export default {
  data() {
    return {
      num
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

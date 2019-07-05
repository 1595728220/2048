<template>
  <div class="pan"  @keyup.up.down.left.right="moveSquare" tabindex="-1">
    <div v-for="(arr,ind) of num" :key="ind" class="colum">
      <my-square :num="value" v-for="(value,index) of arr" :key="index"></my-square>
    </div>
  </div>
</template>
<script>
import Square from "../components/square";
export default {
  data() {
    return {
      //保存数字列表
      num: [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
    };
  },
  methods: {
    //移动方块时触发的事件
    moveSquare() {
      console.log(1)
      this.createTwo()
    },
    // 随机一个下标对象的方法
    ranInd() {
      let x = Math.floor(Math.random() * 4),
        y = Math.floor(Math.random() * 4);
      return { x, y };
    },
    // 产生2的方块的方法
    createTwo() {
      //保存随机下标
      let ind;
      do {
        //获取随机的下标
        ind = this.ranInd();
      } while (
        //要求获取的随机下标不能为有值的方块
        this.num[ind.x][ind.y] !== 0
      );
      //生成新的方块
      this.num = this.num.map((el, index, arr) => {
        //如果x与下标对应
        if (index === ind.x) {
          //修改对应y坐标的值
          el[ind.y] = 2;
        }
        return el;
      });
      console.log(this.num);
    }
  },
  mounted() {
    this.createTwo();
    this.createTwo();
  },
  components: {
    "my-square": Square
  }
};
</script>
<style lang="scss" scoped>
.pan {
  width: 500px;
  height: 500px;
  border-radius: 10px;
  background: #bbada0;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  .colum {
    height: 20%;
    width: 100%;
    display: flex;
    justify-content: space-around;
  }
}
</style>

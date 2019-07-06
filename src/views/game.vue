<template>
  <div class="main">
    <div
      class="pan"
      @keyup.up.down.left.right="moveSquare"
      tabindex="-1"
      @focus="gamePause(true)"
      @blur="gamePause(false)"
      ref="pan"
    >
      <div v-for="(arr,ind) of num" :key="ind" class="colum">
        <my-square :num="value" v-for="(value,index) of arr" :key="index"></my-square>
      </div>
    </div>
    <div class="cloak" v-show="!gameState || !isPlay">
      <button @click="gameStart" v-show="!gameState && !isPlay">点击开始游戏</button>
      <button @click="gamePause(true)" v-show="gameState && !isPlay">继续游戏</button>
      <div v-show="!gameState && isPlay">游戏结束</div>
    </div>
  </div>
</template>
<script>
import Square from "../components/square";
import { setTimeout } from "timers";
export default {
  data() {
    return {
      //保存数字列表
      num: [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]],
      MAXLEN: 4,
      gameState: false,
      isPlay: false
    };
  },
  methods: {
    //移动方块时触发的事件
    moveSquare(e) {
      console.log(e);
      switch (e.key) {
        case "ArrowUp":
          this.squareUp();
          break;
        default:
          console.log("请输入方向键");
      }
      //生成2的方块
      this.createTwo();
    },
    //按下上键触发的向上滑动事件
    squareUp() {
      let tmpNum = this.num;
      //遍历数组
      for (let j = 0; j < this.MAXLEN; j++) {
        for (let i = 1; i < this.MAXLEN; i++) {
          //找到某列第一行不为0的行
          if (tmpNum[i][j] !== 0) {
            //如果前面有0
            if (tmpNum[i - 1][j] === 0) {
              //交换位置
              [tmpNum[i - 1][j], tmpNum[i][j]] = [
                tmpNum[i][j],
                tmpNum[i - 1][j]
              ];
            }
            //如果前面有相同的数字，相加原位置清0
            else if (tmpNum[i][j] === tmpNum[i - 1][j]) {
              tmpNum[i - 1][j] *= 2;
              tmpNum[i][j] = 0;
            }
          }
        }
      }
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
      let ind, tmpNum;
      //将数组转为字符串
      tmpNum = this.num.toString();
      //查找是否全部都不为0
      if (tmpNum.indexOf(0) === -1) {
        //游戏结束
        this.gameEnd();
        return;
      }
      do {
        //获取随机的下标
        ind = this.ranInd();
        console.log(ind);
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
    },
    //游戏开始事件
    gameStart() {
      //游戏进行中
      this.gameState = true;
      //生成两个小方块
      this.createTwo();
      this.createTwo();
      //获取焦点
      this.$refs.pan.focus();
      console.log("游戏开始");
    },
    //游戏暂停
    gamePause(bool) {
      //修改是否正在游戏状态
      this.isPlay = bool;
      if (bool) {
        //获取焦点
        this.$refs.pan.focus();
      } else {
        //失去焦点
        this.$refs.pan.blur();
      }
      console.log("游戏暂停/开始");
    },
    //游戏结束
    gameEnd() {
      //游戏结束
      this.gameState = false;
      console.log("游戏结束");
      //延迟3秒重新开始游戏
      setTimeout(() => {
        //失去焦点
        this.$refs.pan.blur();
        //初始化数字列表
        this.num = [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]];
      }, 3000);
    }
  },
  mounted() {},
  components: {
    "my-square": Square
  }
};
</script>
<style lang="scss" scoped>
.main {
  color: #fff;
  position: relative;
  width: 100vw;
  height: 100vh;
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
    outline: none;
    .colum {
      height: 20%;
      width: 100%;
      display: flex;
      justify-content: space-around;
    }
  }
  .cloak {
    background: rgba(0, 0, 0, 0.3);
    position: absolute;
    width: 100%;
    height: 100%;
    div,button {
      padding: 20px;
      background: khaki;
      color: #fff;
      font-size: 24px;
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
      border: 1px solid khaki;
      outline: none;
      border-radius: 5px;
    }
    div{
      background:#f33;
      border:1px solid #f33;
    }
  }
}
</style>

<template>
    <div :class="'color'+num" class="square">
        {{numCheck}}
    </div>
</template>
<script>
export default {
    props:{
        //方块中显示的数字
        num:{default:0}
    },
    data(){
        return {

        }
    },
    computed: {
        //对数字进行验证和返回
        numCheck(){
            if(this.num === 0) {
                return ""
            }else {
                return this.num
            }
        }
    },

}
</script>
<style lang="scss" scoped>
    .square{
        width:20%;
        border-radius: 5px;
        line-height: 100px;
        font-size:40px;
        transition:all .5s;
    }
</style>

<template>
    <div :class="'color'+num" >
        <p class="color0">{{num}}</p>
    </div>
</template>
<script>
export default {
    props:{
        num:{default:0}
    },
    data(){
        return {

        }
    },

}
</script>
<style lang="scss" scoped>

</style>

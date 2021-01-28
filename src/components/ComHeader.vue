<template>
    <header :style="{backgroundColor:curMenu.bgColor}">
        <span @click="goHome">《 首页</span>
        {{curMenu.name}}
    </header>
</template>

<script>
import { mapState, mapMutations } from "vuex";
    export default {
      computed:{
          ...mapState(["curMenu"]),
      },
      methods:{
          ...mapMutations(["setCurMenu"]),
          goHome(){
              this .$router.push("/");
              this.setCurMenu({
                  name:"剧集",
                  bgColor:"#66ffee"
              });
          },
      },
    };
</script>

<style lang="scss" scoped>
header{
    height: 1rem;
    line-height: 1rem;
    background: rgb(126,23,23);
    text-align: center;
    span{
        position: absolute;
        left:0;
    }
}
</style>
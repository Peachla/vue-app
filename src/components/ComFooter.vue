<template>
    <footer :style="{backgroundColor: curMenu.bgColor}">
        <div  
            v-for=" menu in menuList"
            :key="menu.path"
            @click="switchMenu(menu)"
         > 
            <router-link :to="menu.path">{{menu.name}}</router-link>
        </div>
    </footer>
</template>

<script>
    import { mapState, mapMutations } from "vuex";
    export default {
        computed:{
            ...mapState(["curMenu"]),
        },
        data(){
            return{
                menuList:[
                    { path:"/",name:"剧集",bgColor:"#66ffee"},
                    { path:"/music",name:"音乐",bgColor:"#6644ee"},
                    { path:"/book",name:"书籍",bgColor:"#55ffee"},
                    { path:"/chat",name:"聊天",bgColor:"#6699ee"},
                ],
            };
        },
        methods:{
            ...mapMutations(["setCurMenu"]),
            switchMenu(menu){
                this.setCurMenu(menu)
            },
        },
    };
</script>

<style lang="scss" scoped>
footer{
    display: flex;
    justify-content: space-around;
    position:fixed;
    bottom: 0;
    width: 100%;
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
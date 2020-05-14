<template>
    <div class="theme-wrap" ref="theme-warp" @mouseover="hoverTheme" @mouseout="outTheme" v-drag >
        <img :src="setting" class="setting"/>
        <div class="theme-item" :style="themeStyle(item)"  @click.stop="changeTheme(item)" v-for="(item,index) in data" :key="index"></div>
    </div>
</template>
<script>
    import setting from './settings.png'
    import clickOutside from './directives/clickoutside'
    const normalHeight = 36;
    export default {
        name:"theme",
        props:{
            data:{
                type: Array,
                default () {
                    return [];
                }
            }
        },
        data() {
            return {
                setting,
                open:false,
            }
        },
        directives: {
            drag (el, bindings) {
                var posX
                var posY
                var fwuss = el
                fwuss.onmousedown = function (e) {
                    // 鼠标聚焦
                    fwuss.setCapture && fwuss.setCapture()
                    var disX = (e || event).clientX
                    var disY = (e || event).clientY
                    posX = disX - fwuss.offsetLeft// 获得横坐标x
                    posY = disY - fwuss.offsetTop// 获得纵坐标y
                    // 监听拖拽线高
                    document.onmousemove = function (ev) {
                        // 鼠标距离
                        var iT = (ev || event).clientX - posX
                        var eT = (ev || event).clientY - posY
                        fwuss.style.margin = 0
                        fwuss.style.left = iT + 'px'
                        fwuss.style.right = 'auto';
                        fwuss.style.top = eT + 'px'
                        return false
                    }
                    document.onmouseup = function () {
                        document.onmousemove = null
                        document.onmouseup = null
                        fwuss.releaseCapture && fwuss.releaseCapture()
                    }
                    return false
                }
            },
            clickOutside:clickOutside
        },
        methods:{
            test(){
              alert(111);
            },
            openBox(){
                alert('open');
                this.$refs["theme-warp"].style.height = 'auto';
            },
            closeBox(){
                alert('close');
                this.$refs["theme-warp"].style.height = normalHeight + 'px';
            },
            toggle(){
                this.open = !this.open;
                if(this.open){
                    this.openBox();
                }else {
                    this.closeBox();
                }
            },
            toggleTheme(){
                this.toggle();
            },
            hoverTheme(){
                let height = this.data.length*28 + normalHeight;
                this.$refs["theme-warp"].style.height = height + 'px';
            },
            outTheme(){
                this.$refs["theme-warp"].style.height = normalHeight + 'px';
            },
            changeTheme(item){
                this.$emit("on-changeTheme",item)
            },
            themeStyle(item){
                return{
                    'background-color':item.color
                }
            }
        }
    }
</script>
<style scoped>
    .theme-wrap{
        background-color: #fff;
        width: 38px;
        padding: 8px 0;
        height: 36px;
        border-radius: 4px;
        overflow: hidden;
        text-align: center;
        box-sizing: border-box;
        box-shadow: 0 1px 6px rgba(0,0,0,.2);
        z-index: 900;
        position: fixed;
        right: 10px;
        top: 100px;
        cursor: pointer;
        transition: height .6s ease 0s;
    }
    .theme-wrap:hover img{
        transform: rotate(360deg);;
    }

    .setting{
        width: 16px;
        height: 16px;
        margin-bottom: 10px;
        transition: all .8s ease 0s;
    }
    .theme-item{
        width: 16px;
        height: 16px;
        border: 1px solid #cccccc;
        border-radius: 3px;
        margin: auto;
        margin-bottom: 8px;
        cursor: pointer;

    }
    .theme-item:hover{
        -webkit-box-shadow: 1px 2px 2px hsla(0,0%,0%,.5);
        box-shadow: 1px 2px 2px hsla(0,0%,0%,.5);
    }
</style>

    
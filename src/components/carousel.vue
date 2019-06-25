<template>
<div class="slide" v-on:mouseover="stop()" v-on:mouseout="move()">
    <div class="slideshow" >
          <transition-group tag="ul" name="image"> 
            <li v-for="(item,index) in imglist" 
                v-show="index===mark" 
                :key="index">
                <img :src="item.img" alt="index"> 
            </li>
          </transition-group>
    </div>
    <div class="bar"> 
        <span v-for="(item, index) in imglist" 
              :key="index"
              :class="{'active' : index===mark}"
              @click="change(index)"></span> 
    </div>
</div>
</template>
<script>
export default{
   data () {
       return {
           timer: null,
           mark : 0,
           imglist : [
               {
                    img:'./static/image/img1.jpg'
               },
               {
                    img:'./static/image/img2.jpeg'
               } ,
               {
                    img:'./static/image/img3.jpg'
               },
               {
                    img:'./static/image/img4.jpeg'
               }
           ]
       }
   },
   methods: {
       autoPlay () {
           this.mark++;
           if (this.mark === 4) {
               this.mark = 0;
           }
       },
       play () {
           this.timer=setInterval (this.autoPlay,2000)
       },
       change (i) {
           this.mark = i;
        },
       stop () {
           clearInterval(this.timer)
       },
       move () {
           this.timer = setInterval(this.autoPlay,2000)
       }
   },
    created() {
        this.play();
    }
}
</script>
<style lang="scss" scoped>
    $c-width : 300px;
    $c-height : 150px;
    * { 
        margin: 0; 
        padding: 0; 
        list-style: none; 
    } 
    .slide{
        width : $c-width;
        height : $c-height;
        margin: 0 auto; 
        border : 1px solid #8d8b8b;
        box-shadow: 5px 5px 5px #8d8b8b;
        position: relative;
        overflow : hidden;
    }
    .slideshow {
        width : $c-width;
        height : $c-height;
    }
    li { 
        position: absolute; 
    } 
    img {
        width : $c-width;
        height : $c-height;
    }
    .bar{
        right :10px;
        bottom :10px;
        position: absolute;
        z-index : 99;
    }
    .bar span {
        display: inline-block;
        width: 5px; 
        height: 5px; 
        border-radius: 50%;
        background: #fff;
        margin-right: 10px; 
    }
    .active { 
        background: red !important; 
    } 
    .image-enter-active { 
    transform: translateX(0); 
    transition: all 1.5s ease; 
    } 
    .image-leave-active { 
    transform: translateX(-100%); 
    transition: all 1.5s ease; 
    } 
    .image-enter { 
    transform: translateX(100%); 
    } 
    .image-leave { 
    transform: translateX(0); 
    } 
</style>
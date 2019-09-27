<template>
    <div class="square" @click="flipSquare" :style="squareSize">
        <div v-if="showImg" class="img" :style='backgroundImg' ></div>
        <div v-else class="img" :style="niceBackgroundImg"></div>
    </div>
</template>

<script>
import Vue from 'vue'
import VueYoutube from 'vue-youtube'
 
Vue.use(VueYoutube)

export default {
    name: "Square",
    data: function() {
        return{
            showImg: true,
            videoID: 'tPEE9ZwTmy0'
        }
    },
    props: {
        squareSize: {
            default: {width: 30+'vmin', height: 30+'vmin'}
        },
        backgroundImg: {
            default: ''
        },
        niceBackgroundImg: {
            default: ''
        }
    },
    methods: {
        flipSquare: function(){
            if (this.showImg)
                this.$emit('flipped', this.videoID)
            this.showImg = false
        }
    }

}
</script>

<style scoped>
.square{
    display: grid;
    border: solid;
}
.img{
    width: 100%;
    height: 100%;
    background-size: 70vmin;
}
.vid{
    width: 100%;
    height: auto;
}
</style>

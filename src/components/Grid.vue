<template>
  <div class="grid">
    <div v-if="playingVid">
      <youtube :video-id="videoID" :player-vars="playerVars" @ended="hideVid"></youtube>
    </div>
    <div class="internal-grid" :style="{gridTemplateColumns: 'repeat('+ squaresRoot + ', 1fr)', display: [playingVid? 'none' : 'grid'] }">
      <Square v-for="elem in numSquares" :key="elem" :squareSize=squaresSize :backgroundImg="squareImg(elem, 0)" :niceBackgroundImg="squareImg(elem)" @flipped="showVid" />
    </div>
  </div>
</template>

<script>
import Square from './Square'

export default {
  name: 'Grid',
  components: {
    Square
  },
  data: function() {
    return{
      numSquares: 9,
      imgURL: 'https://i.imgur.com/fHtul15.jpg',
      niceImgURL: 'https://www.wishesgreeting.com/wp-content/uploads/2018/04/Happy-Birthday-Wishes-Cakes.png',
      playingVid: false,
      videoID: "tPEE9ZwTmy0",
      playerVars: {
        autoplay: 1
      }
    }
  },
  computed:{
    squaresRoot: function() {
      return Math.sqrt(this.numSquares)
    },
    squaresSize: function() {
      const size = 70 / this.squaresRoot
      return {
      width: size + 'vmin',
      height: size + 'vmin'
      }
    }
  },
  methods: {
    squareImg: function(ind, nice=1){
      ind = ind-1
      const div = this.squaresRoot - 1
      const x = (ind % this.squaresRoot) * 100 / div
      const y = Math.floor(ind / this.squaresRoot) * 100 / div
      let img
      if (nice)
        img = this.niceImgURL
      else
        img = this.imgURL
      return {
        backgroundImage: 'url(' +img+ ')',
        backgroundPosition: x+'% '+y+'%'
      }
    },
    showVid: function(id){
      this.playingVid = true
      this.videoID = id
    },
    hideVid: function(){
      this.playingVid = false
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.grid{
  display: grid;
  justify-content: center;
  align-content: center;
  background: black;
  min-height: 100%;
}
.internal-grid{
  display: grid;
  grid-gap: 0vmin;
  justify-content: center;
  align-content: center;
  justify-items: center;
  width: fit-content;
}
</style>

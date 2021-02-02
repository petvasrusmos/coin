<template>
  <div :class="{ active__scale: isActive}">
    <!-- isActive: {{isActive}}, heads: {{heads}}, tails:{{tails}} -->
    <div
      class="coin"
      :class="{ tails: tails, heads: heads}"

    >
      <div
       class="coin__front"
       :class="{ tails__img: tails }"
      ></div>
          <div class="coin__edge">
            <div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div>
            <div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div>
            <div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div>
            <div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div>
             <div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div>
            <div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div>
            <div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div>
            <div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div>
          </div>
      <div
        class="coin__back"
        :class="{ heads__img: tails }"
      ></div>
    <!-- <div class="coin__shadow"></div> -->
  </div>
</div>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    isActive: Boolean,
    state: String
  },
  computed: {
    heads () {
      return (this.state === 'heads')
    },
    tails () {
      return (this.state === 'tails')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
$coin-diameter: 300px;
$coin-thickness: 20px;
$coin-color: #f1dd6d;
$coin-front: "../assets/eagle.png";
$coin-back: "../assets/front-coin.png";
$edge-faces: 80;
$edge-face-length: 3.14*$coin-diameter/$edge-faces;
$turn-time: 0.7s;
$iteration-count: 4;

.coin {
  position: relative;
  width: $coin-diameter;
  height: $coin-diameter;
  margin: 50px auto;
}
.tails__img {
  background-image: url($coin-back) !important;
}

.heads__img {
  background-image: url($coin-front) !important;
}
.tails {
  position: relative;
  width: $coin-diameter;
  height: $coin-diameter;
  margin: 50px auto;
  transform-style: preserve-3d;
  animation: rotate3d $turn-time linear $iteration-count;
  transition: all .0.3s;

}
.heads {
  position: relative;
  width: $coin-diameter;
  height: $coin-diameter;
  margin: 50px auto;
  transform-style: preserve-3d;
  animation: rotate3d $turn-time linear $iteration-count;
  transition: all .0.3s;
  // animation-duration: 2s;
  // -webkit-animation-name: flips;
  //  animation-play-state: paused;
}

.active__scale {
  animation: coin-scale $turn-time*$iteration-count linear 1;
}

.coin__front,
.coin__back {
  position: absolute;
  width: $coin-diameter;
  height: $coin-diameter;
  border-radius: 50%;
  overflow: hidden;
  background-color: $coin-color;
  background-repeat: no-repeat;
  transform: translateZ(-$coin-thickness/2) rotateY(180deg);

  &:after {
    content: "";
    position: absolute;
    left: -$coin-diameter/2;
    bottom: 100%;
    display: block;
    height: $coin-diameter/1.5;
    width: $coin-diameter*2;
    background: #fff;
    opacity: 0.3;
    animation: shine linear $turn-time/2 infinite;
  }
}

.coin__front {
  background-image: url($coin-front);
  background-size: 70%;
  background-position: center center;
  transform: translateZ($coin-thickness/2);
}
.coin__back {
  background-image: url($coin-back);
  background-position: center center;
  background-size: 70%;
  transform: translateZ(-$coin-thickness/2) rotateY(180deg);
}

.coin__edge {
  @for $i from 1 through $edge-faces {
    div:nth-child(#{$i}) {
      position: absolute;
      height: $edge-face-length;
      width: $coin-thickness;
      background: darken( $coin-color, ( ($i - $edge-faces/2) * ($i - $edge-faces/2)) / ($edge-faces*$edge-faces/4) * 100 * 0.7 );
      transform:
        translateY(#{$coin-diameter/2-$edge-face-length/2})
        translateX(#{$coin-diameter/2-$coin-thickness/2})
        rotateZ(360deg/$edge-faces*$i+90)
        translateX(#{$coin-diameter/2})
        rotateY(90deg);
    }
  }
}

@keyframes coin-scale {
  from {
    transform: scale(1);
  }
  50% {
    transform: scale(1.8);
  }
  to {
    transform: scale(1);
  }
}
@keyframes rotate3d {
  0% {
    transform: perspective(1000px) rotateX(0deg);
  }
  100% {
    transform: perspective(1000px) rotateX(360deg);
  }
}

// @keyframes shine {
//   0%, 15% {
//     transform: translateY($coin-diameter*2) rotate(-40deg);
//   }
//   50% {
//     transform: translateY(-$coin-diameter) rotate(-40deg);
//   }
// }

</style>

<template>
    <div>
        <div class="watch">
            <!-- Glass -->
            <div class="glass">
                <div class="half-circle"></div>
                <div class="glass-change">
                <h1>14:32</h1>
                <p class="date">29 de setembro d 2020</p>

                <div class="hud">
                  <b-progress :value="life" type="is-danger" show-value format="percent">vida </b-progress>
                  <b-progress class="stats" v-if="hunger > 1" :value="hunger" type="is-warning" show-value format="percent">fome</b-progress>
                  <b-progress class="stats"  v-if="bulletproof > 1" :value="bulletproof" type="is-success" show-value format="percent">colete</b-progress> 
                  <b-progress class="stats" v-if="thirst > 1" :value="thirst" type="is-info" show-value format="percent">sede</b-progress>    
                </div>
                </div>
                <!-- bottom black part -->
                <div class="bottom-black-part"></div>
            </div>

            <!-- belt -->
            <div class="top-belt"></div>
            <div class="bottom-belt"></div>

            <!-- crowns -->
            <div class="first-crown"></div>
            <div class="first-crown-top-shadow"></div>

            <div class="second-crown"></div>
            <div class="second-crown-top-shadow"></div>

        </div>
    </div>
</template>

<script>
export default {
  name: 'smartwatch',
  props: {
    name: {
      type: String,
      required: false,
    },
    life: {
      type: Number,
      required: true,
    },
    hunger: {
      type: Number,
      required: true,
    },
    bulletproof: {
      type: Number,
      required: true,
    },
    thirst: {
      type: Number,
      required: true,
    }
  },
};
</script>

<style scoped>
.watch {
  height: 400px;
  width: 290px;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
}

.glass {
  background: blue;
  background: linear-gradient(#136a89, #257773);
  box-shadow: 0 0 0 3px #202020, 0 0 0 10px #2d3136, 0 0 0 11px #202020;
  border-radius: 50%;
  font-family: Helvetica;
  height: 250px;
  width: 250px;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  margin: auto;
  overflow: hidden;
  z-index: 5;
}

.half-circle {
  display: block;
  position: absolute;
  height: 250px;
  width: 250px;
  background-size: 540px;
}
/*  Crowns
-----------------------------------*/

.first-crown {
  border-bottom-right-radius: 3px;
  border-top-right-radius: 3px;
  height: 25px;
  width: 5px;
  background: #22252a;
  position: absolute;
  top: 191px;
  left: 280px;
  z-index: 4;
}

.first-crown-top-shadow {
  background: #101214;
  border-top-right-radius: 3px;
  position: absolute;
  left: 277px;
  top: 187px;
  height: 8px;
  width: 7px;
  z-index: 3;
}

.second-crown {
  border-top-right-radius: 3px;
  border-bottom-right-radius: 3px;
  height: 20px;
  width: 5px;
  background: #3f444b;
  position: absolute;
  left: 284px;
  top: 194px;
  z-index: 3;
}

.second-crown-top-shadow {
  background: #1f2125;
  border-top-right-radius: 3px;
  position: absolute;
  left: 284px;
  top: 191px;
  height: 6px;
  width: 5px;
  z-index: 2;
}
/*  Belts
-----------------------------------*/

.top-belt {
  background: #22252a;
  border-radius: 7px 7px 0/60px 60px 0;
  height: 120px;
  width: 120px;
  position: absolute;
  left: 84px;
}

.bottom-belt {
  background: #22252a;
  border-radius: 0 7px 7px/0px 0 60px 60px;
  height: 120px;
  width: 120px;
  position: absolute;
  bottom: 0;
  left: 84px;
}
/*  bottom black part
-----------------------------------*/

.bottom-black-part {
  height: 15px;
  width: inherit;
  background: #070707;
  position: absolute;
  bottom: 0;
}
/*  On Display content
-----------------------------------*/

.glass h1,
.glass .date {
  padding-top: 43px;
  text-align: center;
  color: #fff;
  font: 45px Helvetica, "Courier new";
}

.glass .date {
  padding-top: 1px;
  color: #c5dadf;
  font-size: 0.83em;
  letter-spacing: 0.7px;
}

.cloud,
.glass #weather,
.glass .hud {
  position: relative;
  text-align: center;
}

.glass .hud {
  color: #c5dadf;
  top: 20px;
  font: 0.73em Helvetica;
  opacity: 1;
  display: flex;
  flex-direction: row;
}

@-webkit-keyframes opacitys {
  to {
    opacity: 1;
  }
}

@-moz-keyframes opacitys {
  to {
    opacity: 1;
  }
}

@keyframes opacitys {
  to {
    opacity: 1;
  }
}


@-webkit-keyframes fadeIn-clock {
  100% {
    -webkit-transform: translateX(0);
    -moz-transform: translateX(0);
    transform: translateX(0);
  }
}

@-moz-keyframes fadeIn-clock {
  100% {
    -webkit-transform: translateX(0);
    -moz-transform: translateX(0);
    transform: translateX(0);
  }
}

@keyframes fadeIn-clock {
  100% {
    -webkit-transform: translateX(0);
    -moz-transform: translateX(0);
    transform: translateX(0);
  }
}


</style>


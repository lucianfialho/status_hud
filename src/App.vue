<template>
  <div id="app" class="hud" v-if="showSmartWatchHud">
    <div class="container">
      <SmartWatch :life="life" :hunger="hunger" :bulletproof="bulletproof" :thirst="thirst"/>
    </div>
  </div>
</template>

<script>
import SmartWatch from './components/SmartWatch';

export default {
  name: 'app',
  components:{
    SmartWatch
  },
  data() {
    return {
      showSmartWatchHud: false,
      life: 10,
      bulletproof: 0,
      thirst: 0,
      hunger: 0,
    }
  },
  destroyed() {
    window.removeEventListener('message', this.listener);
  },
  mounted() {
    this.listener = window.addEventListener(
      'message',
      event => {
        const item = event.data;

        if(item.showSmartWatchHud === true) this.showSmartWatchHud = true

        if(item.showSmartWatchHud === false) this.showSmartWatchHud = false

        if(item.life) this.life = item.life
        if(item.bulletproof) this.bulletproof = item.bulletproof
        if(item.hunger) this.hunger = item.hunger
        if(item.thirst) this.thirst = item.thirst

      },
      false,
    );
  },
  methods: {},
};
</script>

<style lang="scss">
/* Want nice animations? Check out https://github.com/asika32764/vue2-animate */
/* @import 'https://unpkg.com/vue2-animate/dist/vue2-animate.min.css'; */


html {
  background: transparent;
  overflow-y: hidden;
}

.hud {
    position: fixed;
    bottom: 11.125rem;
    width: 100%;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.hud-person {
  width: 500px;
}

.hud-person .icon {
  height: 0.5rem;
  width: 0.5rem;
  fill: black;
}

.hud-person .another-status .stats {
  width: 31.2%;
  float: left;
  margin: 0.5rem;
 
}
.hud-person .another-status .stats:first-child {
   margin-left: 0rem;
}
.hud-person .another-status .stats:last-child {
   margin-right: 0rem;
}

.gola{fill:#999;}
.armor{fill:#CCCCCC;}

.hud-person .progress-wrapper:not(:last-child) {
  margin-bottom: 0.5rem;
}


.progress{
  width: 50px !important;
  height: 50px !important;
  transform: rotate(-90deg);
  margin-left: 10px;
}

.progress-wrapper .progress-value {
  top: 18px !important;
  left: 35px !important;
}

</style>

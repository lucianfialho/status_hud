<template>
  <div id="app" class="hud" v-if="!playerDead">
    <div class="container">
      <div class="hud-person" v-if="showPersonHud" v-bind:style="`width:${hudSize}`">
        <div class="hud-bar">
          <b-progress :value="life" :size="barWeight" type="is-danger" show-value format="percent">
            {{labels.life}}
          </b-progress>
        </div>
        <div class="hud-bar another-status">
          <b-progress class="stats" :size="barWeight" v-if="hunger > 1"  :value="hunger" type="is-warning" show-value format="percent">
            {{labels.hunger}}
          </b-progress>
          <b-progress class="stats"  :size="barWeight" v-if="bulletproof > 1" :value="bulletproof" type="is-success" show-value format="percent">
            {{labels.armor}}
          </b-progress>    
          <b-progress class="stats" :size="barWeight" v-if="thirst > 1" :value="thirst" type="is-info" show-value format="percent">
            {{labels.thirst}}
          </b-progress>    
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Nui from './utils/Nui'
export default {
  name: 'app',

  data() {
    return {
      showPersonHud: false,
      life: 0,
      bulletproof: 0,
      thirst: 0,
      hunger: 0,
      playerDead: false,
      
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

        if(item.playerDead === true) this.playerDead = true

        if(item.playerDead === false) this.playerDead = false

        if(!item.showPersonHud) this.showPersonHud = true

        if(item.life) this.life = item.life
        if(item.bulletproof) this.bulletproof = item.bulletproof
        if(item.hunger) this.hunger = item.hunger
        if(item.thirst) this.thirst = item.thirst

      },
      false,
    );

    this.loadInterface()
  },
  methods: {
    async loadInterface () {
      const response = await Nui.send('esx_status_hud:loadInterface', { loaded: true })
      const hudInfo = await response.json()
      
      if(hudInfo.playerDead) {
        this.playerDead = true
        return
      }
      
      this.showPersonHud = true
      this.life = hudInfo.life
      this.bulletproof = hudInfo.bulletproof
      this.hunger = hudInfo.hunger
      this.thirst = hudInfo.thirst
      this.hudSize = hudInfo.hudSize
      this.labels = hudInfo.labels
      this.barWeight = hudInfo.barWeight
    }

  },
};
</script>

<style lang="scss">
/* Want nice animations? Check out https://github.com/asika32764/vue2-animate */
/* @import 'https://unpkg.com/vue2-animate/dist/vue2-animate.min.css'; */

@import 'https://fonts.googleapis.com/css2?family=Open+Sans:ital@1&display=swap'; //WEBFONT FROM GOOGLE
html {
  background: transparent;
  overflow-y: hidden;
  
}

.hud {
  position: fixed;
  bottom: 1.125rem;
  width: 100%;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: 'Open Sans', sans-serif; //FONT DECLARATION
}

.hud-person {

  .another-status {
    display: flex;
    .stats {
      width: -webkit-fill-available;
      margin: 0.5rem;
      
      &:first-child{
        margin-left: 0rem;
      }

      &:last-child{
        margin-right: 0rem;
      }
    }
  }
  .progress-wrapper:not(:last-child) {
    margin-bottom: 0.5rem;
  }
}

</style>

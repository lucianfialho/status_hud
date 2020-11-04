<template>
  <div id="app" class="hud" v-if="!playerDead">
    <div class="container">
      {{showPersonHud}}
      {{life}}
      {{bulletproof}}
      {{hunger}}
      {{thirst}}
      {{playerDead}}
      <div class="hud-person" v-if="showPersonHud">
        <div class="hud-bar">
          <b-progress :value="life" type="is-danger" show-value format="percent">
            vida
          </b-progress>
        </div>
        <div class="hud-bar another-status">
          <b-progress class="stats" v-if="hunger > 1"  :value="hunger" type="is-warning" show-value format="percent">
            fome
          </b-progress>
          <b-progress class="stats"  v-if="bulletproof > 1" :value="bulletproof" type="is-success" show-value format="percent">
            colete
          </b-progress>    
          <b-progress class="stats" v-if="thirst > 1" :value="thirst" type="is-info" show-value format="percent">
            sede
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
      const playerInfo = await response.json()
      
      if(playerInfo.playerDead) {
        this.playerDead = true
        return
      }
      
      window.console.log(playerInfo)
      
      this.showPersonHud = true
      this.life = playerInfo.life
      this.bulletproof = playerInfo.bulletproof
      this.hunger = playerInfo.hunger
      this.thirst = playerInfo.thirst
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
  width: 500px;
  .another-status {
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

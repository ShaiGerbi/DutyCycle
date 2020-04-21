<template>
  <div id="app">

    <p>Frequency {{ frequency }}</p>
    <input v-model="frequency" type="range" min="440" max="6000" step="100" value="5000" />

    <p>Width {{ width }}</p>
    <input v-model="width" type="range" min="0" max="1" step="0.1" value="0.5" />

    <button @click="play">play</button>
    <button @click="stop">stop</button>

  </div>
</template>

<script>
import * as Tone from 'tone';

export default {
  name: 'App',

  data() {
    return {
      frequency: 5000,
      width: 0.5,
      tone: null
    }
  },

  methods: {

    play() {
      if(!this.tone) {
        this.tone = new Tone.PulseOscillator ( this.frequency , this.width ).toMaster().start();
      }
      else if (this.tone.state === 'stopped') {
        this.tone = new Tone.PulseOscillator ( this.frequency , this.width ).toMaster().start();
      }
      else {
        this.stop();
        this.tone = new Tone.PulseOscillator ( this.frequency , this.width ).toMaster().start();
      }
    },

    stop() {
      if(this.tone) {
        this.tone.stop();
      }
    },

  }

}
</script>

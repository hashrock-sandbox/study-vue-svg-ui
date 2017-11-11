<template>
  <svg :width="20 * 7 * 4" height="100" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <linearGradient id="svg_4" x1="0.410156" y1="0.417969" x2="0.320313" y2="0.144531">
      <stop stop-color="#fff" offset="0"/>
      <stop stop-color="#b7b7b7" stop-opacity="0.996094" offset="1"/>
      </linearGradient>
      <linearGradient id="svg_10" x1="0.558594" y1="0.785156" x2="0.144531" y2="0">
      <stop stop-color="#666666" offset="0"/>
      <stop stop-color="#ffffff" stop-opacity="0.996094" offset="1"/>
      </linearGradient>
    </defs>
    <g v-for="(white, index) in whites" :key="index" :transform="whitePos(index)" @mousedown="play(white.note)" :class="{'selected': selectedNote === white.note}">
      <rect stroke="#000" id="svg_1" height="100" width="20" x="-0.333333" fill="url(#svg_4)"/>
    </g>
    <g v-for="(black, index) in blacks" :key="index" :transform="blackPos(black.pos)" @mousedown="play(black.note)" :class="{'selected': selectedNote === black.note}">
      <rect fill="#000000" stroke="#000" width="12" height="60" id="svg_5"/>
      <rect fill="#666666" stroke-width="0" x="11" y="0.333334" width="1" height="59" id="svg_6" stroke="#000"/>
      <rect fill="url(#svg_10)" stroke-width="0" x="0.833333" y="56" width="10.5" height="3.666667" id="svg_8" stroke="#000"/>
    </g>
  </svg>
</template>
<script lang="ts">
import Vue from "vue"

var audioContext = new AudioContext();
function mtof(noteNumber: number) {
  return 440 * Math.pow(2, (noteNumber - 69) / 12);
}

function playNote(noteNumber: number, length: number) {
  var osc1 = audioContext.createOscillator();
  var amp = audioContext.createGain();
  var release = 0.05;
  osc1.frequency.value = mtof(noteNumber);
  osc1.connect(amp);
  amp.gain.value = 0.1;
  osc1.start();
  amp.connect(audioContext.destination);
  setTimeout(function() {
    var now = audioContext.currentTime;
    amp.gain.setValueAtTime(amp.gain.value, now);
    amp.gain.linearRampToValueAtTime(0, now + release);
    osc1.stop(now + release);
  }, length);
}

interface Note{
  pos: number
  note: number
}

export default Vue.extend({
  data() {
    return {
      whites: <Note[]>[],
      blacks: <Note[]>[],
      selectedNote: -1
    };
  },
  methods: {
    whitePos(index: number) {
      return `translate(${index * 20},0)`;
    },
    blackPos(index: number) {
      return `translate(${index * 20 + 4},0)`;
    },
    play(note: number) {
      this.selectedNote = note
      playNote(note + 48, 100);
    }
  },
  mounted() {
    function toNote(i: number) {
      return function(n: Note) {
        return {
          pos: n.pos + 7 * i,
          note: n.note + 12 * i
        };
      };
    }

    for (let i = 0; i < 4; i++) {
      this.whites = this.whites.concat(
        [
          { pos: 0, note: 0 },
          { pos: 1, note: 2 },
          { pos: 2, note: 4 },
          { pos: 3, note: 5 },
          { pos: 4, note: 7 },
          { pos: 5, note: 9 },
          { pos: 6, note: 11 }
        ].map(toNote(i))
      );
      this.blacks = this.blacks.concat(
        [
          { pos: 0.5, note: 1 },
          { pos: 1.5, note: 3 },
          { pos: 3.5, note: 6 },
          { pos: 4.5, note: 8 },
          { pos: 5.5, note: 10 }
        ].map(toNote(i))
      );
    }
  }
})
</script>
<style>
.selected rect{
  stroke: blue;
  stroke-width: 2px;
}
</style>



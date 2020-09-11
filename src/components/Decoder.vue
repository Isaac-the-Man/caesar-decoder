<template>
  <div>
    <b-form>
      <b-input-group prepend="Enter Cipher: ">
        <b-form-input v-model="cipher"></b-form-input>
      </b-input-group>
    </b-form>
    <div class="mt-3">
      <b-card class="shadow mt-1" v-for="(decoded, i) in decodedRankedListShow" :key="i">
        <b-row no-gutters>
          <b-col md="1">
            <h3>{{ i + 1 }}.</h3>
          </b-col>
          <b-col md="11">
            {{ decoded.decoded }}
          </b-col>
        </b-row>
      </b-card>
    </div>
    <div class="mt-3 d-flex justify-content-center">
      <b-button v-if="cipher.length > 0" variant="primary" @click="showAll = !showAll">{{ showAll ? 'Show Less' : 'Show All' }}</b-button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Decoder",
  data() {
    return {
      cipher: '',
      freqTable: {
        'E': 0.111607,
        'A': 0.084966,
        'R': 0.075809,
        'I': 0.075448,
        'O': 0.071635,
        'T': 0.069509,
        'N': 0.066544,
        'S': 0.057351,
        'L': 0.054893,
        'C': 0.045388,
        'U': 0.036308,
        'D': 0.033844,
        'P': 0.031671,
        'M': 0.030129,
        'H': 0.030034,
        'G': 0.024705,
        'B': 0.020720,
        'F': 0.018121,
        'Y': 0.017779,
        'W': 0.012899,
        'K': 0.011016,
        'V': 0.010074,
        'X': 0.002902,
        'Z': 0.002722,
        'J': 0.001965,
        'Q': 0.001962
      },
      showAll: false
    }
  },
  computed: {
    cipherUpper() {
      return this.cipher.toUpperCase();
    },
    shiftedList() {
      const list = [];
      if (this.cipher.length > 0) {
        for (let i = 1; i < 26; ++i) {
          list.push(this.shift(this.cipherUpper, i));
        }
      }
      return list;
    },
    decodedRankedList() {
      const rankedList = [];
      for (let entry of this.shiftedList) {
        rankedList.push({
          decoded: entry,
          score: this.scoreDecoded(this.getFreq(this.getStripped(entry)))
        });
      }
      rankedList.sort((a, b) => {
        return a.score - b.score;
      });
      return rankedList;
    },
    decodedRankedListShow() {
      if (this.showAll) {
        return this.decodedRankedList;
      } else {
        return this.decodedRankedList.slice(0, 5)
      }
    }
  },
  methods: {
    getStripped(decoded) {
      // strip space and return uppercase
      const cleaned = decoded.replace(/ /g, '');
      // strip everything that is not a alphabet
      let stripped = '';
      for (let i = 0; i < cleaned.length; i++) {
        if (cleaned.charCodeAt(i) >= 65 && cleaned.charCodeAt(i) <= 90) {
          stripped = stripped + cleaned.charAt(i);
        }
      }
      return stripped;
    },
    getFreq(decoded) {
      // initialize dict with 0
      const dict = {};
      for (let i = 65; i <= 90; i++) {
        dict[String.fromCharCode(i)] = 0;
      }
      if (decoded.length > 0) { // only run if has cipher
        // calculate letter occurrence
        for (let i = 0; i < decoded.length; i++) {
          let char = decoded.charAt(i);
          dict[char] += 1;
        }
        // convert occurrence to frequency
        for (let [key, value] of Object.entries(dict)) {
          dict[key] = Math.round((value * 1000000) / decoded.length) / 1000000;
        }
      }
      return dict;
    },
    scoreDecoded(decodedFreq) {
      let sum = 0;
      for (let [key, value] of Object.entries(this.freqTable)) {
        sum += Math.abs(value - decodedFreq[key]);
      }
      return sum;
    },
    shift(str, n) {
      let shifted = '';
      for (let i = 0; i < str.length; ++i) {
        if (str.charCodeAt(i) >= 65 && str.charCodeAt(i) <= 90) {
          shifted += String.fromCharCode(((str.charCodeAt(i) + n - 65) % 26) + 65);
        } else {
          shifted += str.charAt(i);
        }
      }
      return shifted;
    }
  }
}
</script>

<style scoped>

</style>
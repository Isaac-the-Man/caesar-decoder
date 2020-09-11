<template>
  <div>
    <b-form>
      <b-row no-gutters>
        <b-col md="6">
          <b-input-group prepend="Enter Plaintext: ">
            <b-form-input v-model="plain"></b-form-input>
          </b-input-group>
        </b-col>
        <b-col md="6">
          <b-input-group prepend="Select shift: ">
            <b-form-select v-model="shiftNum" :options="shiftOptions"></b-form-select>
          </b-input-group>
        </b-col>
      </b-row>
    </b-form>
    <div v-if="plain.length > 0" class="mt-3">
      <b>Encrypted Text:</b>
      <div class="mt-1 d-flex align-items-baseline">{{ shift }}
        <b-button class="ml-1" @click="copied = true" pill size="sm" variant="secondary" :data-clipboard-text="shift">copy</b-button>
      </div>
    </div>
    <b-alert class="mt-3" v-model="copied" variant="info" dismissible>
      Copied to Clipboard !
    </b-alert>
  </div>
</template>

<script>
import ClipboardJS from 'clipboard';

export default {
  name: "Encoder",
  data() {
    return {
      plain: '',
      shiftNum: 1,
      copied: false,
      shiftOptions: [
        1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25
      ]
    }
  },
  computed: {
    upper() {
      return this.plain.toUpperCase();
    },
    shift() {
      let shifted = '';
      for (let i = 0; i < this.upper.length; ++i) {
        if (this.upper.charCodeAt(i) >= 65 && this.upper.charCodeAt(i) <= 90) {
          shifted += String.fromCharCode(((this.upper.charCodeAt(i) + this.shiftNum - 65) % 26) + 65);
        } else {
          shifted += this.upper.charAt(i);
        }
      }
      return shifted;
    }
  },
  created() {
    new ClipboardJS('button');
  }
}
</script>

<style scoped>

</style>
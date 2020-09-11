<template>
  <div id="app">
    <b-container class="py-5">
      <b-row>
        <b-col>
          <h1><BIconCodeSlash class="icon"></BIconCodeSlash> Caesar Cipher Decoder</h1>
          A real simple Caesar Cipher decoder using brute force attack. Decoded texts are ranked based on the alphabet
          frequency found
          <b-link href="https://www3.nd.edu/~busiforc/handouts/cryptography/letterfrequencies.html" target="_blank">here</b-link>
          .
          <hr>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <Decoder></Decoder>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <Footer></Footer>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Decoder from "@/components/Decoder";
import Footer from "@/components/Footer";
import { BIconCodeSlash } from 'bootstrap-vue';

export default {
  name: 'App',
  components: {
    Decoder,
    Footer,
    BIconCodeSlash
  }
}
</script>

<style>
  .icon {
    color: #00c853;
  }
</style>

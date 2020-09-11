<template>
  <div id="app">
    <b-container class="py-5">
      <b-row>
        <b-col>
          <h1>Caesar Cipher Decoder</h1>
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

export default {
  name: 'App',
  components: {
    Decoder,
    Footer
  }
}
</script>

<style>
</style>

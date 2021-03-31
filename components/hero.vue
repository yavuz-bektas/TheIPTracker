<template>
<section class="hero is-dark is-fullheight-with-navbar">
  <div class="container">
  <br>
   <b-message type="is-info" has-icon>
      Requests can either be calls to the API, or load events of maps or panoramas. User interactions like zooming or panning are not charged. See Google Maps Platform Billing.
    </b-message>
  </div>
  <div class="hero-body">
    <div class="container has-text-centered">
      <lottie :width="500" :height="500" :options="lottieOptions" v-on:animCreated="handleAnimation" />
    <p class="title ">
      The<strong>IPAdress</strong>Tracker
    </p>
  </div>
  </div>
</section>

</template>

<script>
import lottie from 'vue-lottie/src/lottie.vue'
import * as animationData from "@/assets/map.json";
export default {

  components: {
    lottie
  },
  data() {
    return {
      anim: null, // for saving the reference to the animation
      lottieOptions: { animationData: animationData.default }
    };
  },
  methods: {
    handleAnimation: function (anim) {
      this.anim = anim;
    }
  }
}
</script>


<style>

</style>
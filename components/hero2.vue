<template>
  <section class="hero is-dark is-fullheight-with-navbar">
  <div class="container">

     <section>
        <b-field>
            <b-input type="text"
                :lazy="beLazy"
                size="is-large"
                icon="magnify"
                icon-clickable
                v-model.trim="value"
                @icon-click="searchIconClick"
                placeholder="eg: 8.8.8.8">
            </b-input>
        </b-field>
        <p class="content">
        </p>
    </section>
    <section>
    <div class="tile is-ancestor">
  <div class="tile is-parent">
      <b-message title="CITY & ISP" size="is-large">
            {{city}}<br />
            {{as}}
        </b-message>
  </div>
  <div class="tile is-parent">
      <b-message title="COUNTRY & IP" size="is-large">
            {{country}}<br />
            {{ipadress}}
        </b-message>
  </div>
   <div class="tile is-parent">
      <b-message title="TIMEZONE" size="is-large">
            {{timezone}}
        </b-message>
  </div>
</div>
    </section>
    <br>
<GmapMap
:center="{lat:this.lat, lng:this.lon}"
:zoom="9"
map-type-id="terrain"
style="width: 940px; height: 500px"
>
</GmapMap>
  </div>
  </section>
</template>

<script>
import VueGoogleMaps from '~/plugins/maps.js'
import axios from "axios";
export default {

    data(){
        return{
            beLazy: true,
            value: null,
            city: null,
            as:null,
            country:null,
            ipadress:null,
            timezone:null,
            lat:null,
            lon:null,
        }
    },
    mounted(){
        fetch('http://ip-api.com/json/')
          .then(response => response.json())
          .then(data => {
            this.city = data.city,
            this.as = data.as
            this.country = data.country
            this.ipadress = data.query
            this.timezone = data.timezone
            this.lat=data.lat
            this.lon=data.lon
          });
    },


    methods:{
        searchIconClick(){
            fetch(`http://ip-api.com/json/${this.value}`)
          .then(response => response.json())
          .then(data => {
            this.city = data.city,
            this.as = data.as
            this.country = data.country
            this.ipadress = data.query
            this.timezone = data.timezone
            this.lat=data.lat
            this.lon=data.lon
          });
          this.$buefy.snackbar.open({
                    duration: 5000,
                    message: 'Made with free api. This message will <em>self-destruct</em>.',
                    type: 'is-danger',
                    position: 'is-bottom-left',
                    actionText: 'Undo',
                    queue: false,
                    onAction: () => {
                        this.$buefy.toast.open({
                            message: 'Action pressed',
                            queue: false
                        })
                    }
                })
        },
    },


}
</script>

<style>

</style>
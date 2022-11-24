<!-- <template>
    <div>
    <section class="ui two column centered grid" style="position: relative;z-index:1;">
       <div class="column">
          <form class="ui segment large form">
            <div class="ui message red" v-show="error">{{error}}</div>
            <div class="ui segment">
                <div class="field">
                    <div class="ui right icon input large" :class="{loading:spinner}">
                        <input type="text" 
                        placeholder="enter your adress" 
                        v-model="address"
                        id="autocomplete"
                        />
                        <i class="dot circle link icon" @click="locatorButtonPressed"></i>
                    </div>
                </div>
                <button class="ui button">go</button>
            </div>
          </form>
       </div>
    </section>

    <section id="map"></section>
</div>
 </template>
 
<script>

import axios from 'axios'

   export default {

    data() {
        return {
            address:"",
            error:"",
            spinner: false
        }
    },


    mounted() {
        let autocomplete = new google.maps.places.Autocomplete(
            document.getElementById("autocomplete"),
            {
                bounds: new google.maps.LatLngBounds(
                    new google.maps.LatLng(47.6833,  6.5)
                )
            }

        );

        autocomplete.addListener("place_changed", () => {
        let place = autocomplete.getPlace();
        console.log(place);
        this.showUserLocationOnTheMap(place.geometry.location.lat(), place.geometry.location.lng())
        });
    },


     methods: {
        locatorButtonPressed() {

            this.spinner = true;  
            
            if(navigator.geolocation) {
               navigator.geolocation.getCurrentPosition(
                position => {
                    this.getAdressFrom(
                        position.coords.latitude, 
                        position.coords.longitude);


                        this.showUserLocationOnThemap( 
                        position.coords.latitude, 
                        position.coords.longitude
                        );    
               },

              

               error => {
                this.error = "Locator is unable to find the address. Please type your address manually.";
                this.spinner = false;
                // console.log(error.message);
               }
             );
            } 
            else {
                    this.error = error.message;
                    this.spinner = false;
                    console.log("Your browser does not support geolocation API");
            }
        },
        getAdressFrom(lat, long){
            axios.get("https://maps.googleapis.com/maps/api/geocode/json?latlng=" 
            + lat 
            + "," 
            + long 
            + "&key=AIzaSyBZDJ1KvTvHs0ixS3YOwwhNp-fVZI_olhc")
            .then(response => {
                    if(response.data.error_message) {
                        this.error = response.data.error_message;
                        console.log(response.data.error_message);
                    } else {
                        this.address = response.data.results[0].formatted_address
                        // console.log(response.data.results[0].formatted_address);
                    }
                    this.spinner = false;
            })
            .catch(error => {
                this.error = error.message;
                this.spinner = false;
                console.log(error.message);
            });
        },
        showUserLocationOnThemap(latitude, longitude) {
            //create a map object
            let map = new google.maps.Map(document.getElementById("map"), {
               zoom:15,
               center: new google.maps.LatLng(latitude, longitude),
               mapTypeId: google.maps.MapTypeId.ROADMAP
            });


            // add marker

            new google.maps.Marker({
               position: new google.maps.LatLng(latitude, longitude),
               map: map
            })

        }
     }
   };
</script>





 <style>
    .ui.button,
    .dot.circle.icon {
        background-color: red;
        color: white;
    }

    .pac-icon {
       display: none; 
    }

    .pac-item {
        padding: 10px;
        font-size: 16px;
        cursor: pointer;
    }

    .pac-item:hover{
        background-color: white;
    }

    .pac-item-query {
        font: 16px;
    }

    #map{
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left:0;
        background-color: red;
    }

</style> -->


<template>
    <div>
        <section class="ui two column centered grid" style="position:relative;z-index:1; opacity: 75%;">
        <div class="column">
            <form class="ui segment large form">
                <div class="ui message red" v-show="error">{{error}}</div>
                <div class="ui segment">
                    <div class="field">
                        <div class="ui right icon input large " :class="{loading:spinner}">
                            <input type="text" 
                            placeholder="Entrez votre adresse"
                            v-model="address"
                            id="autocomplete"/>
                            <i class="dot circle link icon " @click="locatorButtonPressed"></i>
                        </div>
                    </div>
                    <button class="ui button blue">go</button>
                </div>
            </form>
        </div>
        </section>

        <section id="map"></section>
    </div>
</template>


<script>

import axios from 'axios'

   export default {

    data() {
        return {
            adress: "",
            error:"",
            spinner: false

        }
    },

    mounted() {
        let autocomplete = new google.maps.places.Autocomplete(
            document.getElementById("autocomplete"),
            {
                bounds: new google.maps.LatLngBounds(
                    new google.maps.LatLng(47.68294, 6.49658)
                )
            });

            autocomplete.addListener("place_changed", () => {
                let place = autocomplete.getPlace();
                console.log(place)
                this.showUserLocationOnTheMap(place.geometry.location.lat(), place.geometry.location.lng())
            });
    },

     methods: {
        locatorButtonPressed() {

            this.spinner = true;

            if(navigator.geolocation) {
               navigator.geolocation.getCurrentPosition(
                position => {
                    this.getAdressFrom(
                        position.coords.latitude, 
                        position.coords.longitude
                    );

                    this.showUserLocationOnTheMap(
                        position.coords.latitude,
                        position.coords.longitude
                    );},

               error => {
                this.error = "Impossible de trouver votre adresse. Veuillez l'écrire manuellement.";
                this.spinner = false;
                // console.log(error.message)
               }
               );
            }

            else {
                this.error = error.message;
                this.spinner = false;
                console.log("Your browser does not support geolocation API");
            }
        },

        getAdressFrom(lat, long){
            axios.get("https://maps.googleapis.com/maps/api/geocode/json?latlng=" 
            + lat 
            + "," 
            + long 
            + "&key=AIzaSyBfRZ3K0R7785Lm5M3p4x78h-ahZ8jRVmQ")

            .then(response => {
                    if(response.data.error_message) {
                        this.error = response.data.error_message;
                        console.log(response.data.error_message);
                    } else {
                        this.address = response.data.results[0].formatted_address
                        // console.log(response.data.results[0].formatted_address);
                    }
                    this.spinner = false;
            })

            .catch(error => {
                this.error = error.message;
                this.spinner = false;
                console.log(error.message);
            });
        },
        showUserLocationOnTheMap(latitude, longitude) {

            let map = new google.maps.Map(document.getElementById("map"), {
            zoom:15,
            center: new google.maps.LatLng(latitude, longitude),
            mapTypeId:  google.maps.MapTypeId.ROADMAP
        });

        new google.maps.Marker({
            position: new google.maps.LatLng(latitude, longitude),
            map:map
        })
        }
     }
   };
</script>


 <style>
    .ui.button,
    .dot.circle.icon {
        background-color: #0F4876;
        color: white;
    }

    .pac-icon{
        display:none;
    }

    .pac-item{
        padding:10px;
        font-size:16px;
        cursor:pointer;
        color: crimson;
    }

    .pac-item:hover{
        background-color: pink;
    }

    .pac-item-query{
        font-size: 16px;
    }

    #map{
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        background-image: url("../assets/gala.jpg");
        background-repeat: no-repeat;
        background-size: cover;
    }
</style>
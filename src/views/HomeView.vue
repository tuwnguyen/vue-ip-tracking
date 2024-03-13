<script setup>
import IPInfo from '@/components/IPInfo.vue'
import leaflet from "leaflet"
import { onMounted } from 'vue';
let mymap
onMounted(() => {
  mymap = leaflet.map('mapid').setView([51.505, -0.09], 13);
  leaflet
        .tileLayer(
          "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoidHV3bmd1eWVuIiwiYSI6ImNsdGZtdjdhMDByd24yam8zbXM3YnN5dGMifQ.pm0fxewcKyC1dYtfKhd-Dg",
          {
            attribution:
              'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
            maxZoom: 18,
            id: "mapbox/streets-v12",
            tileSize: 512,
            zoomOffset: -1,
            accessToken:
              "pk.eyJ1IjoidHV3bmd1eWVuIiwiYSI6ImNsdGZtdjdhMDByd24yam8zbXM3YnN5dGMifQ.pm0fxewcKyC1dYtfKhd-Dg",
          }
        )
        .addTo(mymap);
})
</script>

<template>
  <main>
    <div class="flex flex-col h-screen max-h-screen">
      <!-- Search / Results -->
      <div class="z-20 flex justify-center bg-hero-pattern bg-cover relative px-4 pt-8 pb-32">
        
        <!-- Search Input -->
        <div class="w-full max-w-screen-sm">
          <h1 class="text-white text-center text-3xl pb-4">IP Address Tracker</h1>
          <div class="flex">
            <input 
              type="text"
              class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none"
              placeholder="Search for any IP address or leave empty to get your IP information"
            >
            <i class="fa-solid fa-arrow-right 
            cursor-pointer bg-black text-white rounded-tr-md rounded-br-md flex items-center px-4"></i>
          </div>
        </div>

        <!-- IP Info -->
        <IPInfo />
      </div>

      <!-- Map -->
      <div id="mapid" class="h-full z-10"></div>

    </div>
  </main>
</template>

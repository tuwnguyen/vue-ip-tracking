<script setup>
import IPInfo from '@/components/IPInfo.vue'
import leaflet from "leaflet"
import axios from 'axios';
import { onMounted, ref } from 'vue';
let mymap

const queryIp = ref("")
const ipInfo = ref(null)

onMounted(() => {
  mymap = leaflet.map('mapid').setView([15.9385242,108.4911523,9], 9);
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

const getIpInfo = async () => {
  try {
    const data = await axios.get(`https://geo.ipify.org/api/v2/country,city?apiKey=at_Kk9zYAKBd5P6NFUo8vZhvXJleq0o2&ipAddress=${queryIp.value}`)
    const result = data.data
    ipInfo.value = {
      address: result.ip,
      state: result.location.region,
      timezone: result.location.timezone,
      isp: result.isp,
      lat: result.location.lat,
      lng: result.location.lng
    }
    // leaflet.marker([ipInfo.value.lat, ipInfo.value.lng]).addTo(mymap);
    leaflet.circle([ipInfo.value.lat, ipInfo.value.lng], {
      color: 'red',
      fillColor: '#f03',
      fillOpacity: 0.5,
      radius: 500
    }).addTo(mymap);
    mymap.setView([ipInfo.value.lat, ipInfo.value.lng], 12)
  } catch (e) {
    alert(e.message)
  }
}
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
              v-model="queryIp"
              type="text"
              class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none"
              placeholder="Search for any IP address or leave empty to get your IP information"
            >
            <i 
              @click="getIpInfo"
              class="fa-solid fa-arrow-right 
              cursor-pointer bg-black text-white rounded-tr-md rounded-br-md flex items-center px-4"></i>
          </div>
        </div>

        <!-- IP Info -->
        <IPInfo v-if="ipInfo" :ipInfo/>
      </div>

      <!-- Map -->
      <div id="mapid" class="h-full z-10"></div>

    </div>
  </main>
</template>

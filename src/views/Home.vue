<script setup>
import { onMounted, ref } from "vue";
import axios from 'axios'
import IPInfo from "@/components/IPInfo.vue";
import leaflet from "leaflet";
import "leaflet/dist/leaflet.css";

let myMap
onMounted(() => {
  myMap = leaflet.map("map-id").setView([3.595196, 98.672226], 9)
  leaflet.marker([3.595196, 98.672226]).addTo(myMap);
  leaflet
    .tileLayer(
      `https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=${import.meta.env.VITE_MAPBOX_TOKEN}`,
      {
        attribution:
          'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
        maxZoom: 18,
        id: "mapbox/streets-v11",
        tileSize: 512,
        zoomOffset: -1,
        accessToken: import.meta.env.VITE_MAPBOX_TOKEN,
      }
    )
    .addTo(myMap);
});

const queryIp = ref("")
const ipInfo = ref(null)
const getIpInfo = async() => {
  try{
    // please disable adblock in local dev to test this api
    const response = await axios.get(`https://geo.ipify.org/api/v2/country,city?apiKey=${import.meta.env.VITE_GEO_IPIFY_API_KEY}&ipAddress=${queryIp.value}`)
    const result = response.data
    console.log(response)
    console.log(result)

    ipInfo.value = {
      address: result.ip,
      state: result.location,
      timezone: result.location.timezone,
      isp: result.isp,
      lat: result.location.lat,
      lng: result.location.lng,
    }

    leaflet.marker([result.location.lat, result.location.lng]).addTo(myMap)
    myMap.setView([result.location.lat, result.location.lng], 13);
  }catch(err){
    alert(err.message)
    console.log(err)
  }
}
</script>

<template>
  <div class="flex flex-col h-screen max-h-screen">
    <!-- searh result -->
    <div
      class="relative z-20 flex justify-center px-4 pt-8 pb-32 bg-cover bg-hero-pattern"
    >
      <!-- search input -->
      <div class="w-full max-w-screen-sm">
        <h1 class="pb-4 text-3xl text-center text-white">IP Address Tracker</h1>
        <div class="flex">
          <input
            type="text"
            v-model="queryIp"
            name="ip"
            id="ip"
            class="flex-1 px-2 py-3 rounded-tl-md rounded-bl-md focus:outline-none"
            placeholder="Search for any ip address or leave empty to get your ip info"
          />
          <i
            class="flex items-center px-4 text-white bg-black cursor-pointer fa-solid fa-chevron-right rounded-tr-md rounded-br-md"
            @click="getIpInfo"
          ></i>
        </div>
      </div>

      <!-- IP Info -->
      <IPInfo v-if="ipInfo" :ipInfo="ipInfo"/>
    </div>

    <!-- map -->
    <div id="map-id" class="z-10 h-full"></div>
  </div>
</template>

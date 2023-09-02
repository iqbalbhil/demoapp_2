<script setup>
import Cuaca from "../components/Cuaca.vue";
import Gempa from "../components/Gempa.vue";
import { reactive, onBeforeMount } from "vue";

import {
  IonCard,
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
} from "@ionic/vue";
import { defineComponent } from "vue";
import axios from "axios";

const infoGempa = reactive({ data: {} });
const apiGempa = "https://training28.devbmkg.my.id/gempa-terbaru";

async function fetchGempa(url) {
  const response = await fetch(url);
  const gempa = await response.json();
  infoGempa.data = gempa;
} //Fungsi fetchGempa melakukan fetch data gempa dari url

onBeforeMount(async () => {
  await fetchGempa(apiGempa);
});
</script>
<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Info BMKG</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <main>
        <Cuaca />
        <Gempa :infoGempa="infoGempa.data" />
        <!--  :infoGempa="infoGempa.data" adalah props yang dikirim ke komponen Gempa.vue
          nama variabelnya adalah infoGempa, variabel yang dikirim adalah infoGempa.data
    -->
      </main>
    </ion-content>
  </ion-page>
</template>

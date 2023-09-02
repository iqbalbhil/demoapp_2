<script setup>
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
} from "@ionic/vue";
import CardGempa from "../components/CardGempa.vue";
import { reactive, onMounted } from "vue";
import { Preferences } from "@capacitor/preferences";

const listGempa = reactive({ data: {} });

async function fetchData(url) {
  const resp = await fetch(url);
  const json = await resp.json();
  return json;
}

onMounted(async () => {
  listGempa.data = await fetchData(
    "https://data.bmkg.go.id/DataMKG/TEWS/gempadirasakan.json"
  ); //Fetch daftar 15 gempa yang diraskaan
  listGempa.data = listGempa.data["Infogempa"]["gempa"];
});
</script>
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Gempa</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <main>
        <CardGempa
          v-for="(gempa, index) in listGempa.data"
          :key="index"
          :gempa="gempa"
        />
      </main>
    </ion-content>
  </ion-page>
</template>

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
// import ExploreContainer from "@/components/ExploreContainer.vue";
import CardCuaca from "../components/CardCuaca.vue";
import { cuacaStore } from "../store";
</script>
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Cuaca</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <main>
        <h1 v-if="!cuacaStore.data" class="text-center">
          Silahkan pilih lokasi terlebih dahulu!
        </h1>
        <CardCuaca
          v-else
          v-for="(cuaca, index) in cuacaStore.data['result']"
          :key="index"
          :cuaca="cuaca"
        />
      </main>
    </ion-content>
  </ion-page>
</template>

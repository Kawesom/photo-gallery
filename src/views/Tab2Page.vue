<!-- eslint-disable no-unused-vars -->
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 2</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 2</ion-title>
        </ion-toolbar>
      </ion-header>

        <ion-grid>
          <ion-row>
            <ion-col size="6" :key="photo.filepath" v-for="photo in photos">
              <ion-img :src="photo.webviewPath" @click="showActionSheet(photo)"></ion-img>
            </ion-col>
          </ion-row>
        </ion-grid>

      <ion-content :fullscreen="true">
        <ion-fab vertical="bottom" horizontal="center" slot="fixed">
          <ion-fab-button @click="takePhoto()">
            <ion-icon :icon="camera"></ion-icon>
          </ion-fab-button>
        </ion-fab>
      </ion-content>
    </ion-content>
  </ion-page>
</template>

<script setup>

import { actionSheetController, IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonFab, 
       IonFabButton, IonIcon, IonGrid, IonRow, IonCol, IonImg } from '@ionic/vue';
import { camera, trash, close } from 'ionicons/icons';
import { usePhotoGallery } from '@/composables/usePhotoGallery';

const { takePhoto, photos, deletePhoto } = usePhotoGallery();

const showActionSheet = async (photo) => {
  const actionSheet = await actionSheetController.create({
    header: 'Photos',
    buttons: [
      {
        text: 'Delete',
        role: 'destructive',
        icon: trash,
        handler: () => {
          deletePhoto(photo);
        },
      },
      {
        text: 'Cancel',
        icon: close,
        role: 'cancel',
        handler: () => {
          // Nothing to do, action sheet is automatically closed
        },
      },
    ],
  });
  await actionSheet.present();
};

</script>

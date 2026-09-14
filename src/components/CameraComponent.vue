<template>
  <div class="camera-section">
    <div class="camera-preview">
      <ion-icon :icon="cameraOutline"></ion-icon>
      <p>Ready to capture your moment?</p>
      <span>Tap the button below to take a photo.</span>
    </div>

    <ion-button
      expand="block"
      class="capture-button"
      @click="takePicture"
    >
      <ion-icon slot="start" :icon="cameraOutline"></ion-icon>
      Take Picture
    </ion-button>
  </div>
</template>

<script setup lang="ts">
import {
  Camera,
  CameraResultType,
  CameraSource
} from '@capacitor/camera'

import { cameraOutline } from 'ionicons/icons'

const emit = defineEmits<{
  photoTaken: [photo: string]
}>()

const takePicture = async () => {
  try {
    const image = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.DataUrl,
      source: CameraSource.Camera
    })

    if (image.dataUrl) {
      emit('photoTaken', image.dataUrl)
    }
  } catch (error) {
    console.error('Camera error:', error)
  }
}
</script>

<style scoped>
.camera-section {
  width: 100%;
}

.camera-preview {
  background: #f1e4d4;
  border: 2px dashed #d8c3aa;
  border-radius: 20px;
  padding: 35px 20px;
  text-align: center;
  margin-bottom: 20px;
}

.camera-preview ion-icon {
  font-size: 58px;
  color: #a67c52;
  margin-bottom: 10px;
}

.camera-preview p {
  color: #604832;
  font-size: 17px;
  font-weight: 600;
  margin: 5px 0;
}

.camera-preview span {
  color: #9b846c;
  font-size: 13px;
}

.capture-button {
  --background: #a67c52;
  --background-hover: #8f6845;
  --background-activated: #805d3e;
  --color: #fffaf4;
  --border-radius: 14px;
  --box-shadow: 0 5px 12px rgba(116, 84, 52, 0.18);

  height: 52px;
  font-size: 16px;
  font-weight: 600;
  margin: 0;
}

.capture-button ion-icon {
  font-size: 21px;
}

@media (max-width: 480px) {
  .camera-preview {
    padding: 28px 15px;
  }

  .camera-preview ion-icon {
    font-size: 48px;
  }
}
</style>
<template>
  <div class="camera-section">
    <div class="camera-preview">
      <ion-icon :icon="cameraOutline"></ion-icon>
      <p>Ready to capture your moment?</p>
      <span>Tap the button below to take a photo.</span>
    </div>

    <button
      type="button"
      class="capture-button"
      @click="takePicture"
    >
      <ion-icon :icon="cameraOutline"></ion-icon>
      <span>Take Picture</span>
    </button>
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
  width: 100%;
  height: 52px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;

  background: #a67c52;
  color: #fffaf4;

  border: none;
  border-radius: 14px;

  box-shadow: 0 5px 12px rgba(116, 84, 52, 0.18);

  font-family: inherit;
  font-size: 16px;
  font-weight: 600;

  cursor: pointer;

  transition:
    background 0.2s ease,
    transform 0.2s ease;
}

.capture-button:hover {
  background: #8f6845;
}

.capture-button:active {
  background: #805d3e;
  transform: scale(0.98);
}

.capture-button:focus {
  outline: 3px solid rgba(166, 124, 82, 0.3);
  outline-offset: 3px;
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
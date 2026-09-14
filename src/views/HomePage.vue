<template>
  <ion-page>
    <ion-header class="custom-header">
      <ion-toolbar>
        <ion-title>
          <div class="brand">
            <div class="brand-icon">
              <ion-icon :icon="cameraOutline"></ion-icon>
            </div>

            <span>MyGallery</span>
          </div>
        </ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="gallery-page">
      <div class="page-container">

        <!-- Camera Section -->
        <section class="camera-card">
          <div class="section-heading">
            <div class="section-icon">
              <ion-icon :icon="cameraOutline"></ion-icon>
            </div>

            <div>
              <h2>Capture Photo</h2>
              <p>Take a photo using your camera</p>
            </div>
          </div>

          <CameraComponent @photoTaken="addPhoto" />
        </section>

        <!-- Gallery Section -->
        <section class="gallery-card">
          <div class="gallery-heading">
            <h2>My Gallery</h2>

            <span class="photo-count">
              {{ capturedPhotos.length }} Photos
            </span>
          </div>

          <PhotoGalleryComponent :photos="capturedPhotos" />
        </section>

      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { cameraOutline } from 'ionicons/icons'

import CameraComponent from '../components/CameraComponent.vue'
import PhotoGalleryComponent from '../components/PhotoGalleryComponent.vue'

const capturedPhotos = ref<string[]>([])

// Add new captured photo
const addPhoto = (photo: string) => {
  capturedPhotos.value.unshift(photo)

  localStorage.setItem(
    'snapgallery-photos',
    JSON.stringify(capturedPhotos.value)
  )
}

// Load saved photos when the page opens or reloads
onMounted(() => {
  const savedPhotos = localStorage.getItem('snapgallery-photos')

  if (savedPhotos) {
    capturedPhotos.value = JSON.parse(savedPhotos)
  }
})
</script>

<style scoped>
ion-content.gallery-page {
  --background: #f3eadf;
}

.custom-header ion-toolbar {
  --background: #f8f1e8;
  --color: #4d3929;
  --border-color: #e4d5c3;
  --border-width: 0 0 1px 0;
}

.brand {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 24px;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.brand-icon {
  width: 48px;
  height: 48px;
  border-radius: 14px;
  background: #a67c52;
  color: #fffaf4;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 27px;
}

.page-container {
  max-width: 850px;
  margin: 0 auto;
  padding: 24px 18px 40px;
}

.camera-card,
.gallery-card {
  background: #fffaf4;
  border-radius: 28px;
  padding: 24px;
  margin-bottom: 24px;
  box-shadow: 0 8px 25px rgba(116, 84, 52, 0.08);
}

.section-heading {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-bottom: 24px;
}

.section-icon {
  width: 64px;
  height: 64px;
  border-radius: 18px;
  background: #eee0ce;
  color: #805d3e;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 32px;
}

h2 {
  color: #4d3929;
  margin: 0;
  font-size: 25px;
  font-weight: 700;
}

.section-heading p {
  color: #927a61;
  margin: 5px 0 0;
  font-size: 15px;
}

.gallery-heading {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}

.photo-count {
  background: #eee0ce;
  color: #604832;
  padding: 9px 16px;
  border-radius: 20px;
  font-size: 14px;
  font-weight: 600;
  white-space: nowrap;
}

@media (max-width: 480px) {
  .page-container {
    padding: 18px 12px 30px;
  }

  .camera-card,
  .gallery-card {
    padding: 18px;
    border-radius: 22px;
  }

  .brand {
    font-size: 21px;
  }

  .brand-icon {
    width: 42px;
    height: 42px;
    font-size: 23px;
  }

  h2 {
    font-size: 21px;
  }

  .section-icon {
    width: 52px;
    height: 52px;
    font-size: 27px;
  }

  .section-heading p {
    font-size: 13px;
  }
}
</style>
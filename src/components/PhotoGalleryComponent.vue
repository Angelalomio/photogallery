<template>
  <div class="gallery-wrapper">
    <!-- Empty Gallery -->
    <div v-if="photos.length === 0" class="empty-gallery">
      <ion-icon :icon="imagesOutline"></ion-icon>
      <h3>No Photos Yet</h3>
      <p>Your captured photos will appear here.</p>
    </div>

    <!-- Photo Gallery -->
    <div v-else class="gallery">
      <ion-card
        v-for="(photo, index) in photos"
        :key="index"
        class="photo-card"
      >
        <img
          :src="photo"
          :alt="`Captured photo ${index + 1}`"
        />
      </ion-card>
    </div>
  </div>
</template>

<script setup lang="ts">
import { imagesOutline } from 'ionicons/icons'

defineProps<{
  photos: string[]
}>()
</script>

<style scoped>
.gallery-wrapper {
  width: 100%;
}

.gallery {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 14px;
}

.photo-card {
  margin: 0;
  padding: 0;
  border-radius: 18px;
  overflow: hidden;
  background: #f1e4d4;
  box-shadow: 0 5px 15px rgba(116, 84, 52, 0.08);
}

.photo-card img {
  display: block;
  width: 100%;
  height: auto;
  max-height: 260px;
  object-fit: contain;
  background: #eadbc9;
}

.empty-gallery {
  text-align: center;
  padding: 45px 20px;
  border: 2px dashed #d8c3aa;
  border-radius: 20px;
  background: #fcf7f0;
}

.empty-gallery ion-icon {
  font-size: 55px;
  color: #b99b7a;
}

.empty-gallery h3 {
  color: #604832;
  margin: 12px 0 6px;
  font-size: 20px;
}

.empty-gallery p {
  color: #a08a73;
  margin: 0;
  font-size: 14px;
}

@media (max-width: 480px) {
  .gallery {
    gap: 10px;
  }

  .photo-card {
    border-radius: 14px;
  }

  .photo-card img {
    max-height: 220px;
  }
}
</style>
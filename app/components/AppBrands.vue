<template>
  <section class="brands">
    <div class="brands__header">
      <h2>Trabalhamos com as <span>Melhores Marcas</span></h2>
    </div>

    <div class="brands__carousel">
      <div class="brands__track">
        <div class="brand-item" v-for="(brand, index) in duplicatedBrands" :key="index">
          <span class="brand-placeholder">{{ brand.name }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue';

const brandList = [
  { name: 'VOTORANTIM' },
  { name: 'TIGRE' },
  { name: 'SUVINIL' },
  { name: 'MAKITA' },
  { name: 'BOSCH' },
  { name: 'DECA' },
  { name: 'TRAMONTINA' }
];

const duplicatedBrands = computed(() => [...brandList, ...brandList, ...brandList, ...brandList]);
</script>

<style lang="scss" scoped>
@use "sass:color";

.brands {
  padding: 4rem 0;
  background-color: $dark-background; 
  border-top: 1px solid color.scale($light-text, $lightness: -80%);
  border-bottom: 1px solid color.scale($light-text, $lightness: -80%);
  overflow: hidden; 

  &__header {
    text-align: center;
    margin-bottom: 3rem;

    h2 {
      font-size: 2rem;
      color: $light-text;
      text-transform: uppercase;
      letter-spacing: 1px;

      span {
        color: $primary-color;
      }
    }
  }

  &__carousel {
    width: 100%;
    overflow: hidden;
    position: relative;
    mask-image: linear-gradient(to right, transparent, black 10%, black 90%, transparent);
    -webkit-mask-image: linear-gradient(to right, transparent, black 10%, black 90%, transparent);
  }

  &__track {
    display: flex;
    gap: 4rem; 
    width: max-content;
    animation: scrollBrands 30s linear infinite;

    &:hover {
      animation-play-state: paused;
    }
  }

  .brand-item {
    display: flex;
    align-items: center;
    justify-content: center;
    
    .brand-placeholder {
      font-size: 1.5rem;
      font-weight: 800;
      color: color.scale($light-text, $lightness: -40%);
      transition: color 0.3s ease;
      cursor: default;

      &:hover {
        color: $primary-color;
      }
    }
  }
}

@keyframes scrollBrands {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}
</style>
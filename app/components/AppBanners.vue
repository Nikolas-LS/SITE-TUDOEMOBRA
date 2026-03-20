<template>
  <section class="banners-section" v-if="banners.length > 0">
    <div class="banners-container">
      
      <header class="section-header">
        <div class="yellow-bar"></div>
        <h2>Ofertas <span>Exclusivas</span></h2>
        <p>Aproveite os melhores preços direto da nossa loja.</p>
      </header>

      <div class="carousel-wrapper">
        
        <div 
          class="carousel-track" 
          :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
        >
          <div 
            v-for="banner in banners" 
            :key="banner.id" 
            class="carousel-item"
          >
            <img :src="banner.image_url" :alt="banner.title" />
            
            <div class="item-content-card">
              <h3>{{ banner.title }}</h3>
              <button class="btn-oferta">Ver Detalhes →</button>
            </div>
          </div>
        </div>

        <button class="nav-btn prev" @click="prevSlide" aria-label="Slide Anterior">‹</button>
        <button class="nav-btn next" @click="nextSlide" aria-label="Próximo Slide">›</button>

        <div class="carousel-pagination">
          <button 
            v-for="(banner, index) in banners" 
            :key="'dot-' + index"
            :class="['dot', { active: index === currentIndex }]"
            @click="goToSlide(index)"
            :aria-label="'Ir para slide ' + (index + 1)"
          ></button>
        </div>
      </div>

    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const supabase = useSupabaseClient()
const banners = ref([])
const currentIndex = ref(0)
const autoplayInterval = ref(null)

const fetchBanners = async () => {
  const { data, error } = await supabase
    .from('banners')
    .select('*')
    .order('created_at', { ascending: false })
  
  if (!error) banners.value = data
}

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % banners.value.length
}

const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + banners.value.length) % banners.value.length
}

const goToSlide = (index) => {
  currentIndex.value = index
}

// --- AUTOPLAY ---
const startAutoplay = () => {
  autoplayInterval.value = setInterval(nextSlide, 5000) 
}

const stopAutoplay = () => {
  if (autoplayInterval.value) clearInterval(autoplayInterval.value)
}

// Ciclo de vida: Inicia busca e autoplay
onMounted(async () => {
  await fetchBanners()
  if (banners.value.length > 1) startAutoplay()
})

onUnmounted(stopAutoplay)
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap');

.banners-section {
  padding: 6rem 5%;
  background-color: #f8f9fa; 
  font-family: 'Inter', sans-serif;
  overflow: hidden; 
}

.banners-container {
  max-width: 1400px; 
  margin: 0 auto;
  position: relative;
}

.section-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  margin-bottom: 4rem;

  .yellow-bar {
    width: 60px;
    height: 5px;
    background: $primary-color;
    border-radius: 10px;
    margin-bottom: 1rem;
  }

  h2 {
    font-size: 2.8rem;
    font-weight: 800;
    color: $dark-background;
    margin: 0;
    text-transform: uppercase;
    letter-spacing: -1px;

    span { color: $primary-color; }
  }

  p {
    color: #636e72;
    font-size: 1.1rem;
    margin-top: 0.5rem;
  }
}

.carousel-wrapper {
  position: relative;
  width: 100%;
  border-radius: 20px;
  overflow: hidden; 
  box-shadow: 0 20px 50px rgba(0,0,0,0.1);
}

.carousel-track {
  display: flex;
  width: 100%;
  transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1); 
}

.carousel-item {
  min-width: 100%; 
  width: 100%;
  height: 500px; 
  position: relative;
  
  img {
    width: 100%;
    height: 100%;
    object-fit: cover; 
  }
}

.item-content-card {
  position: absolute;
  bottom: 40px;
  left: 40px;
  background: rgba(255, 255, 255, 0.9); 
  backdrop-filter: blur(10px); 
  padding: 2.5rem;
  border-radius: 16px;
  max-width: 450px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.1);
  border: 1px solid rgba(255,255,255,0.3);

  h3 {
    font-size: 2rem;
    font-weight: 800;
    color: $dark-background; 
    margin: 0 0 1.5rem 0;
    line-height: 1.1;
  }

  .btn-oferta {
    background: $primary-color;
    color: $dark-background;
    border: none;
    padding: 0.8rem 1.8rem;
    font-weight: 700;
    font-size: 1rem;
    border-radius: 8px;
    cursor: pointer;
    transition: 0.3s;
    font-family: inherit;

    &:hover {
      background: $dark-background;
      color: white;
      transform: translateY(-2px);
    }
  }
}

.nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.7);
  color: $dark-background;
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  font-size: 2rem;
  font-weight: 300;
  line-height: 45px;
  cursor: pointer;
  transition: 0.3s;
  z-index: 10;
  backdrop-filter: blur(5px);

  &:hover { background: $primary-color; color: $dark-background; }
  &.prev { left: 20px; }
  &.next { right: 20px; }
}

.carousel-pagination {
  position: absolute;
  bottom: 20px;
  right: 40px;
  display: flex;
  gap: 8px;
  z-index: 10;

  .dot {
    width: 12px;
    height: 12px;
    background: rgba(255, 255, 255, 0.5);
    border: 2px solid white;
    border-radius: 50%;
    cursor: pointer;
    padding: 0;
    transition: 0.3s;

    &.active {
      background: $primary-color;
      border-color: $primary-color;
      width: 30px; 
      border-radius: 10px;
    }
  }
}

@media (max-width: 768px) {
  .section-header h2 { font-size: 2.2rem; }
  .carousel-item { height: 400px; }
  .item-content-card {
    bottom: 20px; left: 20px; right: 20px;
    padding: 1.5rem;
    max-width: none;
    text-align: center;
    h3 { font-size: 1.5rem; }
  }
  .nav-btn { display: none; } 
  .carousel-pagination { right: 50%; transform: translateX(50%); }
}
</style>
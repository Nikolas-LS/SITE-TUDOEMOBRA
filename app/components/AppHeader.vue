<template>
  <header :class="['header', { 'header--scrolled': isScrolled }]">
    
<div class="header__logo">
      <NuxtLink to="/" @click="scrollTo('#hero')">
        <img 
          src="/logo-tudoemobra.png" 
          alt="Logo TUDOEMOBRA" 
          class="logo-img" 
        />
      </NuxtLink>
    </div>
    
    <nav class="header__nav">
      <a href="#hero" @click.prevent="scrollTo('#hero')">Início</a>
      <a href="#ofertas" @click.prevent="scrollTo('#ofertas')">Ofertas</a>
      <a href="#departments" @click.prevent="scrollTo('#departments')">Departamentos</a>
      <a href="#brands" @click.prevent="scrollTo('#brands')">Marcas</a>
      <a href="#about" @click.prevent="scrollTo('#about')">Sobre Nós</a>
      <a href="#contact" @click.prevent="scrollTo('#contact')">Contato</a>
    </nav>

    <div class="header__action">
      <button class="btn-primary desktop-btn">Fale no WhatsApp</button>
      
      <button class="menu-toggle" @click="toggleMenu" aria-label="Menu">
        <span class="bar" :class="{ 'bar-1': isMenuOpen }"></span>
        <span class="bar" :class="{ 'bar-2': isMenuOpen }"></span>
        <span class="bar" :class="{ 'bar-3': isMenuOpen }"></span>
      </button>
    </div>
    
    <div class="mobile-overlay" v-if="isMenuOpen" @click="toggleMenu"></div>
    
    <nav :class="['mobile-menu', { 'mobile-menu--open': isMenuOpen }]">
      <div class="mobile-menu__header">
        <img src="/logo-tudoemobra.png" alt="Logo" class="mobile-logo" />
        <button class="close-btn" @click="toggleMenu">✕</button>
      </div>
      
      <div class="mobile-menu__links">
        <a href="#home" @click.prevent="handleMobileNav('#hero')">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path><polyline points="9 22 9 12 15 12 15 22"></polyline></svg>
          Início
        </a>
        <a href="#ofertas" @click.prevent="handleMobileNav('#ofertas')">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20.59 13.41l-7.17 7.17a2 2 0 0 1-2.83 0L2 12V2h10l8.59 8.59a2 2 0 0 1 0 2.82z"></path><line x1="7" y1="7" x2="7.01" y2="7"></line></svg>
          Ofertas
        </a>
        <a href="#departments" @click.prevent="handleMobileNav('#departments')">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
          Departamentos
        </a>
        <a href="#brands" @click.prevent="handleMobileNav('#brands')">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"></polygon></svg>
          Marcas
        </a>
        <a href="#about" @click.prevent="handleMobileNav('#about')">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path><circle cx="9" cy="7" r="4"></circle><path d="M23 21v-2a4 4 0 0 0-3-3.87"></path><path d="M16 3.13a4 4 0 0 1 0 7.75"></path></svg>
          Sobre Nós
        </a>
        <a href="#contact" @click.prevent="handleMobileNav('#contact')">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
          Contato
        </a>
      </div>
      
      <div class="mobile-menu__footer">
        <button class="btn-primary w-100">Fale no WhatsApp</button>
      </div>
    </nav>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMenuOpen = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
  document.body.style.overflow = isMenuOpen.value ? 'hidden' : 'auto'
}

const scrollTo = (selector) => {
  const element = document.querySelector(selector)
  if (element) {
    const headerOffset = 80 
    const elementPosition = element.getBoundingClientRect().top
    const offsetPosition = elementPosition + window.scrollY - headerOffset

    window.scrollTo({
      top: offsetPosition,
      behavior: 'smooth'
    })
  }
}

const handleMobileNav = (selector) => {
  toggleMenu()
  setTimeout(() => scrollTo(selector), 300)
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style lang="scss" scoped>
@use "sass:color";
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@500;600;700&display=swap');

:global(html) {
  scroll-behavior: smooth;
}

/* O BOTÃO GERAL FOI MOVIDO PARA CIMA PARA SER REAPROVEITADO NO MENU MOBILE */
.btn-primary {
  background-color: $primary-color;
  color: $dark-background; /* Cor do texto conforme seu código base */
  border: none;
  padding: 0.8rem 1.8rem;
  font-size: 0.95rem;
  font-weight: 700;
  font-family: inherit; 
  border-radius: 6px; 
  cursor: pointer;
  transition: transform 0.3s ease, background-color 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  justify-content: center;
  align-items: center;

  &:hover {
    transform: translateY(-2px); 
    background-color: color.scale($primary-color, $lightness: 5%);
    box-shadow: 0 5px 15px rgba(243, 156, 18, 0.3); 
  }

  &.w-100 {
    width: 100%;
    padding: 1rem; /* Um pouco mais alto no celular para ficar fácil de clicar */
    font-size: 1.05rem;
  }
}

.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 5%; 
  background-color: $dark-background;
  border-bottom: 2px solid $primary-color;
  transition: all 0.3s ease; 
  font-family: 'Montserrat', sans-serif; 

  &--scrolled {
    padding: 0.3rem 5%; 
    background-color: rgba($dark-background, 0.95);
    backdrop-filter: blur(10px);
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    border-bottom-color: transparent; 
  }

  &__logo {
    display: flex;
    align-items: center;
    .logo-img {
      max-height: 85px;   
      width: auto;
      object-fit: contain;
      transition: transform 0.3s ease;
      &:hover { transform: scale(1.02); }
    }
  }

  &__nav {
    display: flex;
    gap: 2.5rem;
    a {
      color: $light-text;
      text-decoration: none;
      font-weight: 600;
      font-size: 1rem;
      letter-spacing: 0.5px;
      position: relative;
      transition: color 0.3s ease;

      &::after {
        content: '';
        position: absolute;
        bottom: -4px;
        left: 0;
        width: 0%;
        height: 2px;
        background-color: $primary-color;
        transition: width 0.3s ease;
      }

      &:hover {
        color: $primary-color;
        &::after { width: 100%; }
      }
    }
  }

  &__action {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
}

/* Toggle do Menu Hamburguer */
.menu-toggle {
  display: none; 
  background: transparent;
  border: none;
  cursor: pointer;
  flex-direction: column;
  justify-content: space-around;
  width: 32px;
  height: 24px;
  padding: 0;
  z-index: 1001;

  .bar {
    width: 100%;
    height: 3px;
    background-color: $primary-color;
    border-radius: 10px;
    transition: all 0.3s ease;
    transform-origin: 1px;
  }
  
  .bar-1 { transform: rotate(45deg); }
  .bar-2 { opacity: 0; }
  .bar-3 { transform: rotate(-45deg); }
}

/* Overlay Escuro cobrindo o cabeçalho (z-index maior que 1000) */
.mobile-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(4px);
  z-index: 1001; 
}

/* Menu Mobile (z-index máximo para cobrir o overlay e o cabeçalho) */
.mobile-menu {
  position: fixed;
  top: 0;
  right: -320px; 
  width: 320px;
  max-width: 85vw;
  height: 100vh;
  background-color: #1a1a1a; 
  box-shadow: -5px 0 30px rgba(0,0,0,0.5);
  z-index: 1002; 
  display: flex;
  flex-direction: column;
  transition: right 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  padding: 2rem;
  font-family: 'Montserrat', sans-serif;

  &--open {
    right: 0; 
  }

  &__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 2.5rem;
    border-bottom: 1px solid rgba(255,255,255,0.05);
    padding-bottom: 1.5rem;

    .mobile-logo { max-height: 45px; }
    
    .close-btn {
      background: none;
      border: none;
      color: #cbd5e1;
      font-size: 1.8rem;
      cursor: pointer;
      transition: color 0.3s;
      &:hover { color: $primary-color; }
    }
  }

  &__links {
    display: flex;
    flex-direction: column;
    gap: 1.2rem;
    flex-grow: 1;

    a {
      display: flex;
      align-items: center;
      gap: 1rem;
      color: #f1f5f9;
      text-decoration: none;
      font-size: 1.1rem;
      font-weight: 500;
      padding: 0.8rem;
      border-radius: 8px;
      transition: all 0.3s ease;
      
      svg { width: 22px; height: 22px; opacity: 0.7; transition: opacity 0.3s; }

      &:hover { 
        background-color: rgba(243, 156, 18, 0.1); 
        color: $primary-color; 
        svg { opacity: 1; color: $primary-color; }
      }
    }
  }

  &__footer {
    margin-top: auto;
    padding-top: 1rem;
  }
}

@media (max-width: 992px) {
  .header {
    padding: 1rem 5%;
    
    &__nav { display: none; } 
    .desktop-btn { display: none; } 
    .menu-toggle { display: flex; } 
    
    .logo-img { max-height: 55px; }
  }
}
</style>
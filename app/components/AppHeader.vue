<template>
  <header class="header">
    <div class="header__logo">
      <h1>TUDO<span>EM</span>OBRA</h1>
    </div>
    
    <nav class="header__nav">
      <a href="#home">Início</a>
      <a href="#departments">Departamentos</a>
      <a href="#about">Sobre Nós</a>
      <a href="#contact">Contato</a>
    </nav>

    <div class="header__action">
      <button class="btn-primary">Fale no WhatsApp</button>
    </div>
  </header>
</template>

<style lang="scss" scoped>

@use "sass:color";

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 5%;
  background-color: $dark-background;
  border-bottom: 2px solid $primary-color;

  &__logo {
    h1 {
      font-size: 1.8rem;
      color: $light-text;
      letter-spacing: 1px;
      
      span {
        color: $primary-color;
      }
    }
  }

  &__nav {
    display: flex;
    gap: 2rem;

    a {
      color: $light-text;
      text-decoration: none;
      font-weight: 500;
      transition: color 0.3s ease;

      &:hover {
        color: $primary-color;
      }
    }
  }

  &__action {
    .btn-primary {
      background-color: $primary-color;
      color: $dark-background;
      border: none;
      padding: 0.8rem 1.5rem;
      font-size: 1rem;
      font-weight: bold;
      border-radius: 4px;
      cursor: pointer;
      transition: transform 0.2s ease, background-color 0.3s ease;

      &:hover {
        transform: scale(1.05);
        background-color: color.scale($primary-color, $lightness: -15%);
      }
    }
  }
}

@media (max-width: 768px) {
  .header {
    flex-direction: column;
    gap: 1rem;
    
    &__nav {
      display: none;
    }
  }
}
</style>
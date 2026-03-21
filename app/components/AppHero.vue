<template>
  <section class="hero" id="hero">
    <div class="hero__content">
      <h2 class="hero__title">A Base Forte para a <span>Sua Obra</span></h2>
      <p class="hero__description">
        Encontre os melhores materiais de construção com qualidade, agilidade e o atendimento especializado que você e seu projeto merecem.
      </p>
      <div class="hero__actions">
        <button class="btn-primary">Fazer Orçamento</button>
        <button class="btn-secondary">Nossos Departamentos</button>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
@use "sass:color";

.hero {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;  
  padding: 2rem 5%;
  text-align: center;
  
  background: linear-gradient(
      rgba($dark-background, 0.85), 
      rgba($dark-background, 0.95)
    ), 
    url('https://images.pexels.com/photos/159306/construction-site-build-construction-work-159306.jpeg?auto=compress&cs=tinysrgb&w=1920&q=80') center/cover no-repeat;
  
  &__content {
    max-width: 800px;
    z-index: 1;
    animation: fadeIn 1s ease-out forwards;
  }

  &__title {
    font-size: 3.5rem;
    color: $light-text;
    margin-bottom: 1.5rem;
    line-height: 1.2;
    text-transform: uppercase;

    span {
      color: $primary-color;
    }
  }

  &__description {
    font-size: 1.2rem;
    color: $light-background;
    margin-bottom: 2.5rem;
    line-height: 1.6;
  }

  &__actions {
    display: flex;
    gap: 1.5rem;
    justify-content: center;

    button {
      padding: 1rem 2rem;
      font-size: 1.1rem;
      font-weight: bold;
      border-radius: 4px;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    .btn-primary {
      background-color: $primary-color;
      color: $dark-background;
      border: none;

      &:hover {
        transform: translateY(-3px);
        background-color: color.scale($primary-color, $lightness: -15%);
      }
    }

    .btn-secondary {
      background-color: transparent;
      color: $primary-color;
      border: 2px solid $primary-color;

      &:hover {
        transform: translateY(-3px);
        background-color: $primary-color;
        color: $dark-background;
      }
    }
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 768px) {
  .hero {
    min-height: 100vh; 
    
    &__title {
      font-size: 2.2rem;
    }
    
    &__actions {
      flex-direction: column;
      gap: 1rem;
    }
  }
}
</style>
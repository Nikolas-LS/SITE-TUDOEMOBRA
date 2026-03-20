<template>
  <section class="about" id="about">
    <div class="about__container">
      
      <div class="about__image-wrapper">
        <img 
          src="https://images.pexels.com/photos/224924/pexels-photo-224924.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&q=80" 
          alt="Estrutura de obra da TUDOEMOBRA" 
          class="about__image"
        />
        <div class="about__image-decoration"></div>
      </div>

      <div class="about__content">
        <h4 class="about__subtitle">Nossa História</h4>
        <h2 class="about__title">Tradição e Inovação na <span>Construção Civil</span></h2>
        
        <p class="about__text">
          A <strong>TUDOEMOBRA</strong> nasceu com um propósito claro: ser a parceira definitiva de construtores, arquitetos e famílias que estão realizando o sonho da casa própria. Entendemos que cada tijolo importa e que o tempo é valioso em uma obra.
        </p>
        
        <p class="about__text">
          Com anos de experiência no mercado, oferecemos não apenas um catálogo completo de materiais brutos e acabamentos finos, mas um atendimento consultivo de quem realmente entende de construção. Da fundação ao telhado, nossa excelência é a sua garantia de uma obra segura e no prazo.
        </p>

        <ul class="about__features">
          <li>
            <span class="icon">✓</span>
            Entregas Rápidas e Seguras
          </li>
          <li>
            <span class="icon">✓</span>
            Atendimento Especializado
          </li>
          <li>
            <span class="icon">✓</span>
            As Melhores Marcas do Mercado
          </li>
        </ul>

        <button class="btn-primary">Fale com um Especialista</button>
      </div>

    </div>
  </section>
</template>

<style lang="scss" scoped>
@use "sass:color";

.about {
  min-height: 100vh;
  padding: 6rem 5%;
  background-color: $light-background;
  display: flex;
  align-items: center;
  justify-content: center;

  &__container {
    display: grid;
    grid-template-columns: 1fr 1fr; 
    gap: 4rem;
    max-width: 1200px;
    width: 100%;
    align-items: center; 
  }

  &__image-wrapper {
    position: relative;
    width: 100%;
    max-width: 500px;
    margin: 0 auto;
  }

  &__image {
    width: 100%;
    height: auto;
    border-radius: 8px;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
    position: relative;
    z-index: 2; 
  }

  &__image-decoration {
    position: absolute;
    top: -20px;
    left: -20px;
    width: 100%;
    height: 100%;
    background-color: $primary-color;
    border-radius: 8px;
    z-index: 1;
  }

  &__content {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }

  &__subtitle {
    color: $primary-color;
    font-size: 1.2rem;
    text-transform: uppercase;
    letter-spacing: 2px;
    margin-bottom: 0.5rem;
  }

  &__title {
    font-size: 2.5rem;
    color: $dark-background;
    margin-bottom: 1.5rem;
    line-height: 1.2;

    span {
      color: $primary-color;
    }
  }

  &__text {
    font-size: 1.1rem;
    color: color.scale($dark-text, $lightness: 20%);
    margin-bottom: 1.5rem;
    line-height: 1.6;

    strong {
      color: $dark-background;
    }
  }

  &__features {
    list-style: none;
    margin-bottom: 2.5rem;

    li {
      font-size: 1.1rem;
      color: $dark-background;
      margin-bottom: 0.8rem;
      display: flex;
      align-items: center;
      gap: 0.8rem;

      .icon {
        color: $primary-color;
        font-weight: bold;
        font-size: 1.2rem;
      }
    }
  }

  .btn-primary {
    background-color: $primary-color;
    color: $dark-background;
    border: none;
    padding: 1rem 2rem;
    font-size: 1.1rem;
    font-weight: bold;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.3s ease;

    &:hover {
      transform: translateY(-3px);
      background-color: color.scale($primary-color, $lightness: -15%);
    }
  }
}

@media (max-width: 992px) {
  .about__container {
    grid-template-columns: 1fr; 
    gap: 3rem;
  }

  .about__image-wrapper {
    order: 2; 
    margin-top: 2rem;
  }

  .about__content {
    order: 1; 
    align-items: center; 
    text-align: center;
  }

  .about__features li {
    justify-content: center; 
  }
}
</style>
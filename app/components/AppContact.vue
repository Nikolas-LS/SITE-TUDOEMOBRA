<template>
  <section class="contact" id="contact">
    <div class="contact__container">
      
      <div class="contact__info">
        <h4 class="contact__subtitle">Fale Conosco</h4>
        <h2 class="contact__title">Visite Nossa <span>Loja</span></h2>
        
        <p class="contact__desc">
          Nossa equipe de especialistas está pronta para ajudar a calcular materiais e fazer o melhor orçamento para a sua obra. Venha tomar um café com a gente!
        </p>

        <ul class="contact__details">
          <li>
            <span class="icon">📍</span>
            <div>
              <strong>Endereço</strong>
              <p>Av. Imperatriz Leopoldina, 1000 - São Leopoldo, RS</p>
            </div>
          </li>
          <li>
            <span class="icon">📞</span>
            <div>
              <strong>Telefone & WhatsApp</strong>
              <p>(51) 99999-0000</p>
            </div>
          </li>
          <li>
            <span class="icon">⏰</span>
            <div>
              <strong>Horário de Funcionamento</strong>
              <p>Seg a Sex: 07:30 - 18:00<br>Sáb: 08:00 - 12:00</p>
            </div>
          </li>
        </ul>

        <button class="btn-primary">Enviar Mensagem no WhatsApp</button>
      </div>

      <div class="contact__map-wrapper">
        <iframe 
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d13854.409384978713!2d-51.14421115!3d-29.7603348!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x951968878e1b4395%3A0x7d6c6e76bc688fc9!2sS%C3%A3o%20Leopoldo%2C%20RS!5e0!3m2!1spt-BR!2sbr!4v1710892000000!5m2!1spt-BR!2sbr" 
          width="100%" 
          height="100%" 
          style="border:0;" 
          allowfullscreen
          loading="lazy" 
          referrerpolicy="no-referrer-when-downgrade"
          class="contact__map"
        ></iframe>
      </div>

    </div>
  </section>
</template>

<style lang="scss" scoped>
@use "sass:color";

.contact {
  padding: 6rem 5%;
  background-color: $dark-background;
  color: $light-text;
  display: flex;
  align-items: center;
  justify-content: center;

  &__container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
    max-width: 1200px;
    width: 100%;
  }

  &__info {
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
    margin-bottom: 1.5rem;
    line-height: 1.2;

    span {
      color: $primary-color;
    }
  }

  &__desc {
    font-size: 1.1rem;
    color: color.scale($light-text, $lightness: -30%);
    margin-bottom: 2.5rem;
    line-height: 1.6;
  }

  &__details {
    list-style: none;
    margin-bottom: 2.5rem;
    width: 100%;

    li {
      display: flex;
      align-items: flex-start;
      gap: 1.2rem;
      margin-bottom: 1.5rem;
      padding-bottom: 1.5rem;
      border-bottom: 1px solid color.scale($light-text, $lightness: -80%);

      &:last-child {
        border-bottom: none;
      }

      .icon {
        font-size: 1.8rem;
        background-color: color.scale($dark-background, $lightness: 10%);
        padding: 0.8rem;
        border-radius: 8px;
        color: $primary-color;
      }

      strong {
        display: block;
        font-size: 1.1rem;
        margin-bottom: 0.3rem;
        color: $light-text;
      }

      p {
        font-size: 1rem;
        color: color.scale($light-text, $lightness: -30%);
        line-height: 1.4;
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
    width: 100%;

    &:hover {
      background-color: color.scale($primary-color, $lightness: -15%);
    }
  }

  &__map-wrapper {
    width: 100%;
    min-height: 400px;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.5);
    border: 2px solid color.scale($dark-background, $lightness: 10%);
  }

  &__map {
    width: 100%;
    height: 100%;
    filter: invert(90%) hue-rotate(180deg) brightness(80%) contrast(100%);
  }
}

@media (max-width: 992px) {
  .contact__container {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
}
</style>
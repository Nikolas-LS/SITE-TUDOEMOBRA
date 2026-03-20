<template>
  <footer class="footer">
    <div class="footer__container">
      
      <div class="footer__brand">
        <div class="footer__logo">TUDO<span>EM</span>OBRA</div>
        <p class="footer__desc">
          A base forte para a sua construção. Qualidade, confiança e agilidade em um só lugar.
        </p>
      </div>

      <div class="footer__links">
        <h4>Navegação</h4>
        <nav>
          <a href="#home">Início</a>
          <a href="#departments">Departamentos</a>
          <a href="#about">Sobre Nós</a>
          <a href="#contact">Contato</a>
        </nav>
      </div>

      <div class="footer__social">
        <h4>Siga-nos</h4>
        <div class="social-links">
          <a href="#" target="_blank" rel="noopener">Instagram</a>
          <a href="#" target="_blank" rel="noopener">Facebook</a>
          <a href="#" target="_blank" rel="noopener">LinkedIn</a>
        </div>
      </div>

    </div>

    <div class="footer__bottom">
      <p>© 2026 Tudo em Obra Materiais de Construção. Todos os direitos reservados.</p>
      <p class="dev-credit">Desenvolvido com excelência por você.</p>
    </div>
  </footer>
</template>

<style lang="scss" scoped>
@use "sass:color";

.footer {
  background-color: color.scale($dark-background, $lightness: -10%);
  color: $light-text;
  padding: 4rem 5% 1rem 5%;
  border-top: 2px solid $primary-color;

  &__container {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr;
    gap: 3rem;
    max-width: 1200px;
    margin: 0 auto;
    padding-bottom: 3rem;
    border-bottom: 1px solid color.scale($light-text, $lightness: -80%);
  }

  &__logo {
    font-size: 1.8rem;
    font-weight: 900;
    letter-spacing: 1px;
    margin-bottom: 1rem;

    span {
      color: $primary-color;
    }
  }

  &__desc {
    color: color.scale($light-text, $lightness: -30%);
    line-height: 1.6;
    max-width: 300px;
  }

  h4 {
    color: $light-text;
    font-size: 1.2rem;
    margin-bottom: 1.5rem;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  &__links nav,
  &__social .social-links {
    display: flex;
    flex-direction: column;
    gap: 0.8rem;

    a {
      color: color.scale($light-text, $lightness: -30%);
      text-decoration: none;
      transition: all 0.3s ease;
      width: fit-content;

      &:hover {
        color: $primary-color;
        transform: translateX(5px);
      }
    }
  }

  &__bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto;
    padding-top: 1.5rem;
    font-size: 0.9rem;
    color: color.scale($light-text, $lightness: -50%);

    .dev-credit {
      color: color.scale($light-text, $lightness: -40%);
    }
  }
}

@media (max-width: 768px) {
  .footer {
    &__container {
      grid-template-columns: 1fr;
      gap: 2rem;
      text-align: center;
    }

    &__desc {
      margin: 0 auto;
    }

    &__links nav,
    &__social .social-links {
      align-items: center;
    }

    &__bottom {
      flex-direction: column;
      gap: 1rem;
      text-align: center;
    }
  }
}
</style>
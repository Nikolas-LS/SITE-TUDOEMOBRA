<template>
  <section class="departments" id="departments">
    <div class="departments__header">
      <h2>Nossos <span>Departamentos</span></h2>
      <p>Tudo o que você precisa, do alicerce ao acabamento, em um só lugar.</p>
    </div>

    <div class="departments__grid">
      <div 
        class="card" 
        v-for="dept in departmentList" 
        :key="dept.id"
      >
        <div class="card__icon">{{ dept.icon }}</div>
        <h3 class="card__title">{{ dept.name }}</h3>
        <p class="card__desc">{{ dept.desc }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>

const departmentList = [
  { id: 1, name: 'Bruto', desc: 'Cimento, areia, brita, tijolos e blocos estruturais.', icon: '🧱' },
  { id: 2, name: 'Ferramentas', desc: 'Equipamentos manuais e elétricos de alta performance.', icon: '🔨' },
  { id: 3, name: 'Elétrica', desc: 'Fios, cabos, disjuntores, conduítes e iluminação.', icon: '⚡' },
  { id: 4, name: 'Hidráulica', desc: 'Tubos, conexões, registros e caixas d\'água.', icon: '💧' },
  { id: 5, name: 'Ferragens', desc: 'Pregos, parafusos, dobradiças e fechaduras seguras.', icon: '🔩' },
  { id: 6, name: 'Acabamentos', desc: 'Pisos, porcelanatos, tintas e revestimentos.', icon: '🎨' }
];
</script>

<style lang="scss" scoped>
@use "sass:color";

.departments {
  min-height: 100vh;
  padding: 5rem 5%;
  background-color: $light-background; 
  color: $dark-text;
  display: flex;
  flex-direction: column;
  justify-content: center;

  &__header {
    text-align: center;
    margin-bottom: 4rem;

    h2 {
      font-size: 2.8rem;
      color: $dark-background;
      margin-bottom: 1rem;
      text-transform: uppercase;

      span {
        color: $primary-color;
      }
    }

    p {
      font-size: 1.2rem;
      color: color.scale($dark-text, $lightness: 20%);
    }
  }

  &__grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 2rem;
    width: 100%;
    max-width: 1200px;
    margin: 0 auto; 
  }

  .card {
    background-color: $light-text;
    padding: 2.5rem 1.5rem;
    border-radius: 8px;
    text-align: center;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
    border-bottom: 4px solid transparent;
    transition: all 0.3s ease;

    &:hover {
      transform: translateY(-10px);
      box-shadow: 0 15px 25px rgba(0, 0, 0, 0.1);
      border-bottom: 4px solid $primary-color;
    }

    &__icon {
      font-size: 3.5rem;
      margin-bottom: 1.5rem;
    }

    &__title {
      font-size: 1.5rem;
      color: $dark-background;
      margin-bottom: 1rem;
    }

    &__desc {
      font-size: 1rem;
      color: $dark-text;
      line-height: 1.5;
    }
  }
}

@media (max-width: 768px) {
  .departments {
    &__header h2 {
      font-size: 2.2rem;
    }
  }
}
</style>
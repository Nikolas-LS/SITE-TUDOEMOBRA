<template>
  <div class="login-page">
    <div class="login-card">
      <div class="logo">TUDO<span>EM</span>OBRA</div>
      <h2>Acesso Administrativo</h2>
      <p>Entre com suas credenciais para gerenciar o site.</p>

      <form @submit.prevent="handleLogin" class="login-form">
        <div class="form-group">
          <label>E-mail</label>
          <input type="email" v-model="email" required placeholder="seu@email.com" />
        </div>

        <div class="form-group">
          <label>Senha</label>
          <input type="password" v-model="password" required placeholder="••••••••" />
        </div>

        <button type="submit" :disabled="loading" class="btn-login">
          {{ loading ? 'Autenticando...' : 'Entrar no Painel' }}
        </button>
      </form>

      <p v-if="errorMsg" class="error-alert">{{ errorMsg }}</p>
      
      <NuxtLink to="/" class="btn-back">← Voltar para a Loja</NuxtLink>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const router = useRouter()

const email = ref('')
const password = ref('')
const loading = ref(false)
const errorMsg = ref('')

const handleLogin = async () => {
  loading.value = true
  errorMsg.value = ''

  const { error } = await supabase.auth.signInWithPassword({
    email: email.value,
    password: password.value,
  })

  if (error) {
    errorMsg.value = 'E-mail ou senha inválidos.'
    loading.value = false
  } else {
    // Login com sucesso! Redireciona para o admin
    router.push('/admin')
  }
}
</script>

<style lang="scss" scoped>
.login-page {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f4f7f6;
  font-family: 'Inter', sans-serif;
  padding: 2rem;
}

.login-card {
  background: white;
  padding: 3rem;
  border-radius: 20px;
  box-shadow: 0 20px 40px rgba(0,0,0,0.05);
  width: 100%;
  max-width: 400px;
  text-align: center;

/* No seu arquivo login.vue, procure a classe .logo e deixe assim: */
.logo {
  font-size: 1.8rem;
  font-weight: 900;
  margin-bottom: 1.5rem;
  color: #2d3436; /* Isso vai fazer o TUDO e o OBRA aparecerem em cinza escuro */
  
  span { 
    color: $primary-color; 
  }
}

  h2 { font-size: 1.5rem; color: #2d3436; margin-bottom: 0.5rem; }
  p { color: #636e72; font-size: 0.9rem; margin-bottom: 2rem; }
}

.login-form {
  text-align: left;
  .form-group {
    margin-bottom: 1.2rem;
    label { display: block; font-size: 0.8rem; font-weight: 700; margin-bottom: 0.4rem; color: #2d3436; }
    input {
      width: 100%;
      padding: 0.8rem;
      border: 2px solid #edf2f7;
      border-radius: 8px;
      &:focus { border-color: $primary-color; outline: none; }
    }
  }
}

.btn-login {
  width: 100%;
  background: $primary-color;
  color: $dark-background;
  border: none;
  padding: 1rem;
  border-radius: 8px;
  font-weight: 700;
  cursor: pointer;
  transition: 0.3s;
  margin-top: 1rem;
  &:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(243, 156, 18, 0.2); }
}

.error-alert { color: #ff7675; font-size: 0.85rem; margin-top: 1rem; font-weight: 600; }

.btn-back {
  display: inline-block;
  margin-top: 2rem;
  text-decoration: none;
  color: #b2bec3;
  font-size: 0.85rem;
  &:hover { color: $dark-background; }
}
</style>
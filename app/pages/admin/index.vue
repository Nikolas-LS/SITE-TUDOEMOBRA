<template>
  <div class="admin-dashboard">
    <div class="admin-container">
      
      <header class="admin-header">
        <div class="header-content">
          <NuxtLink to="/" class="btn-back">
            <span class="arrow">←</span> Voltar para o Site
          </NuxtLink>
          <h1>Painel <span>Administrativo</span></h1>
          <p>Gestão de Banners e Ofertas da TUDOEMOBRA</p>
        </div>
      </header>

      <div class="admin-grid">
        <aside class="upload-column">
          <div class="glass-card">
            <div class="card-header">
              <div class="yellow-bar"></div>
              <h3>Novo Banner</h3>
            </div>
            
            <form @submit.prevent="handleUpload" class="upload-form">
              <div class="form-group">
                <label>Título do Banner</label>
                <input type="text" v-model="title" required placeholder="Ex: Cimento em Promoção" />
              </div>

              <div class="form-group">
                <label>Selecione a Imagem</label>
                <div class="file-input-wrapper">
                  <input type="file" @change="onFileChange" accept="image/*" required id="fileInput" />
                </div>
              </div>

              <button type="submit" class="btn-submit" :disabled="isUploading">
                <span v-if="!isUploading">Publicar Agora</span>
                <span v-else class="loader">Processando...</span>
              </button>
            </form>

            <div v-if="message" :class="['alert', messageType]">{{ message }}</div>
          </div>
        </aside>

        <main class="list-column">
          <div class="glass-card">
            <div class="card-header">
              <div class="yellow-bar"></div>
              <h3>Banners Ativos <span>({{ banners.length }})</span></h3>
            </div>
            
            <div v-if="loadingList" class="loading-state">
              <p>Buscando dados no servidor...</p>
            </div>
            
            <div v-else class="banners-list">
              <TransitionGroup name="list">
                <div v-for="banner in banners" :key="banner.id" class="banner-item">
                  <div class="banner-preview">
                    <img :src="banner.image_url" />
                  </div>
                  <div class="banner-info">
                    <h4>{{ banner.title }}</h4>
                    <span class="date">{{ formatDate(banner.created_at) }}</span>
                  </div>
                  <button @click="deleteBanner(banner)" class="btn-delete-icon" title="Excluir Banner">
                    Excluir
                  </button>
                </div>
              </TransitionGroup>

              <div v-if="banners.length === 0" class="empty-state">
                <p>Nenhum banner ativo no momento.</p>
              </div>
            </div>
          </div>
        </main>
      </div>
    </div>
  </div>
</template>

<script setup>
// (O script permanece com a mesma lógica do Supabase, 
// apenas adicionei uma funçãozinha de formatar data para o novo design)
import { ref, onMounted } from 'vue'
const supabase = useSupabaseClient()

const title = ref('')
const file = ref(null)
const isUploading = ref(false)
const loadingList = ref(true)
const banners = ref([])
const message = ref('')
const messageType = ref('')

const fetchBanners = async () => {
  loadingList.value = true
  const { data, error } = await supabase.from('banners').select('*').order('created_at', { ascending: false })
  if (!error) banners.value = data
  loadingList.value = false
}

const onFileChange = (e) => { file.value = e.target.files[0] }

const handleUpload = async () => {
  if (!file.value) return
  isUploading.value = true
  try {
    const fileExt = file.value.name.split('.').pop()
    const fileName = `${Date.now()}.${fileExt}`
    const { error: uploadError } = await supabase.storage.from('banners').upload(fileName, file.value)
    if (uploadError) throw uploadError
    const { data: { publicUrl } } = supabase.storage.from('banners').getPublicUrl(fileName)
    const { error: dbError } = await supabase.from('banners').insert([{ title: title.value, image_url: publicUrl }])
    if (dbError) throw dbError
    message.value = 'Sucesso! Banner adicionado.'
    messageType.value = 'success'
    title.value = ''; file.value = null; document.getElementById('fileInput').value = '';
    fetchBanners()
  } catch (e) {
    message.value = 'Erro: ' + e.message
    messageType.value = 'error'
  } finally { isUploading.value = false }
}

const deleteBanner = async (banner) => {
  if (!confirm(`Excluir "${banner.title}"?`)) return
  try {
    const fileName = banner.image_url.split('/').pop()
    await supabase.storage.from('banners').remove([fileName])
    const { error } = await supabase.from('banners').delete().eq('id', banner.id)
    if (error) throw error
    fetchBanners()
  } catch (e) { alert('Erro: ' + e.message) }
}

const formatDate = (dateString) => {
  return new Date(dateString).toLocaleDateString('pt-BR')
}

onMounted(fetchBanners)
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap');

.admin-dashboard {
  min-height: 100vh;
  background: #f8f9fa;
  font-family: 'Inter', sans-serif;
  color: #2d3436;
  padding: 2rem 1rem;
}

.admin-container {
  max-width: 1200px;
  margin: 0 auto;
}

.admin-header {
  margin-bottom: 3rem;
  .btn-back {
    text-decoration: none;
    color: #636e72;
    font-size: 0.9rem;
    font-weight: 600;
    transition: 0.3s;
    &:hover { color: $primary-color; }
  }
  h1 {
    font-size: 2.2rem;
    font-weight: 800;
    margin: 0.5rem 0;
    span { color: $primary-color; }
  }
  p { color: #636e72; font-size: 1rem; }
}

.admin-grid {
  display: grid;
  grid-template-columns: 350px 1fr;
  gap: 2rem;
}

.glass-card {
  background: white;
  border-radius: 16px;
  padding: 2rem;
  box-shadow: 0 10px 30px rgba(0,0,0,0.04);
  border: 1px solid #edf2f7;
}

.card-header {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 2rem;
  .yellow-bar {
    width: 6px;
    height: 24px;
    background: $primary-color;
    border-radius: 10px;
  }
  h3 {
    margin: 0;
    font-size: 1.2rem;
    font-weight: 700;
    color: #2d3436; // Cor do texto forçada aqui!
    span { color: #b2bec3; font-weight: 400; font-size: 1rem; }
  }
}

.upload-form {
  .form-group {
    margin-bottom: 1.5rem;
    label {
      display: block;
      font-size: 0.85rem;
      font-weight: 700;
      margin-bottom: 0.5rem;
      color: #636e72; // Cor do label forçada aqui!
    }
    input[type="text"] {
      width: 100%;
      padding: 0.8rem;
      border: 2px solid #edf2f7;
      border-radius: 8px;
      transition: 0.3s;
      &:focus { border-color: $primary-color; outline: none; }
    }
  }
}

.btn-submit {
  width: 100%;
  background: $primary-color;
  color: $dark-background;
  border: none;
  padding: 1rem;
  border-radius: 8px;
  font-weight: 700;
  cursor: pointer;
  transition: 0.3s;
  &:hover:not(:disabled) { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(243, 156, 18, 0.3); }
  &:disabled { opacity: 0.6; cursor: not-allowed; }
}

/* Estilos da Lista de Itens */
.banner-item {
  display: flex;
  align-items: center;
  padding: 1rem;
  background: #fff;
  border: 1px solid #edf2f7;
  border-radius: 12px;
  margin-bottom: 1rem;
  transition: 0.3s;
  
  &:hover { border-color: $primary-color; }

  .banner-preview {
    width: 100px;
    height: 60px;
    border-radius: 8px;
    overflow: hidden;
    margin-right: 1.5rem;
    img { width: 100%; height: 100%; object-fit: cover; }
  }

  .banner-info {
    flex: 1;
    h4 { margin: 0; font-size: 1rem; font-weight: 700; }
    .date { font-size: 0.8rem; color: #b2bec3; }
  }
}

.btn-delete-icon {
  background: #fff5f5;
  color: #ff7675;
  border: 1px solid #fab1a0;
  padding: 0.5rem 1rem;
  border-radius: 6px;
  font-weight: 600;
  font-size: 0.8rem;
  cursor: pointer;
  transition: 0.3s;
  &:hover { background: #ff7675; color: white; }
}

.alert {
  margin-top: 1.5rem;
  padding: 1rem;
  border-radius: 8px;
  text-align: center;
  font-size: 0.9rem;
  font-weight: 600;
  &.success { background: #e6fffa; color: #2c7a7b; }
  &.error { background: #fff5f5; color: #c53030; }
}

/* Animação da Lista */
.list-enter-active, .list-leave-active { transition: all 0.4s ease; }
.list-enter-from, .list-leave-to { opacity: 0; transform: translateX(30px); }

@media (max-width: 900px) {
  .admin-grid { grid-template-columns: 1fr; }
}
</style>
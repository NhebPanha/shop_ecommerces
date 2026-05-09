<template>
  <div class="products-page">
    <div class="page-header">
      <div class="title">
        <h2>Products</h2>
        <p>Manage your inventory and product listings</p>
      </div>
      <button class="add-btn" @click="openModal()">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="M12 5v14"/></svg>
        Add Product
      </button>
    </div>

    <div class="filters glass">
      <div class="search-box">
        <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.3-4.3"/></svg>
        <input type="text" v-model="globalSearch" placeholder="Search products..." />
      </div>
      <div class="filter-actions">
        <div class="category-pills">
          <button 
            v-for="cat in categories" 
            :key="cat"
            class="pill" 
            :class="{ active: selectedCategory === cat }"
            @click="selectedCategory = cat"
          >
            {{ cat }}
          </button>
        </div>
        <select class="sort-select" v-model="sortBy">
          <option value="newest">Newest First</option>
          <option value="price-asc">Price: Low to High</option>
          <option value="price-desc">Price: High to Low</option>
        </select>
      </div>
    </div>

    <div class="products-grid">
      <ProductCard 
        v-for="product in filteredProducts" 
        :key="product.id" 
        :product="product" 
        @edit="openModal(product)"
        @delete="deleteProduct(product.id)"
      />
    </div>

    <!-- Add/Edit Modal -->
    <Modal 
      :show="showModal" 
      :title="isEditing ? 'Edit Product' : 'Add New Product'"
      :submitText="isEditing ? 'Update Product' : 'Add Product'"
      @close="showModal = false"
      @submit="handleSave"
    >
      <div class="form-group">
        <label>Product Name</label>
        <input type="text" v-model="form.name" placeholder="e.g. iPhone 15 Pro" />
      </div>
      <div class="form-row">
        <div class="form-group">
          <label>Category</label>
          <select v-model="form.category">
            <option v-for="cat in categories.filter(c => c !== 'All')" :key="cat" :value="cat">{{ cat }}</option>
          </select>
        </div>
        <div class="form-group">
          <label>Price ($)</label>
          <input type="number" v-model="form.price" step="0.01" />
        </div>
      </div>
      <div class="form-group">
        <label>Stock Quantity</label>
        <input type="number" v-model="form.stock" />
      </div>
      <div class="form-group">
        <label>Product Image</label>
        <div class="upload-area" @click="$refs.fileInput.click()">
          <input type="file" ref="fileInput" hidden @change="handleFileUpload" />
          <img v-if="form.image" :src="form.image" class="preview-img" />
          <div v-else class="upload-placeholder">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" x2="12" y1="3" y2="15"/></svg>
            <span>Click to upload image</span>
          </div>
        </div>
      </div>
    </Modal>
  </div>
</template>

<script setup>
const globalSearch = useGlobalSearch()
const selectedCategory = ref('All')
const sortBy = ref('newest')
const categories = ['All', 'Electronics', 'Fashion', 'Home']

const products = ref([])

onMounted(() => {
  const savedProducts = localStorage.getItem('products')
  if (savedProducts) {
    products.value = JSON.parse(savedProducts)
  } else {
    // Initial dummy data if nothing is saved
    products.value = [
      { id: 1, name: 'iPhone 15 Pro Max', category: 'Electronics', price: 1199.00, stock: 45, status: 'Active', image: 'https://images.unsplash.com/photo-1696446701796-da61225697cc?q=80&w=500' },
      { id: 2, name: 'MacBook Air M3', category: 'Electronics', price: 1299.00, stock: 12, status: 'Active', image: 'https://images.unsplash.com/photo-1517336714731-489689fd1ca8?q=80&w=500' },
      { id: 3, name: 'Leather Messenger Bag', category: 'Fashion', price: 185.00, stock: 8, status: 'Low', image: 'https://images.unsplash.com/photo-1548036328-c9fa89d128fa?q=80&w=500' },
      { id: 4, name: 'Sony WH-1000XM5', category: 'Electronics', price: 349.00, stock: 24, status: 'Active', image: 'https://images.unsplash.com/photo-1505740420928-5e560c06d30e?q=80&w=500' },
      { id: 5, name: 'Ceramic Coffee Set', category: 'Home', price: 45.00, stock: 0, status: 'Out', image: 'https://images.unsplash.com/photo-1580915411954-282cb1b0d780?q=80&w=500' },
    ]
    saveToStorage()
  }
})

function saveToStorage() {
  localStorage.setItem('products', JSON.stringify(products.value))
}

const filteredProducts = computed(() => {
  let result = products.value.filter(p => {
    const matchesSearch = p.name.toLowerCase().includes(globalSearch.value.toLowerCase())
    const matchesCategory = selectedCategory.value === 'All' || p.category === selectedCategory.value
    return matchesSearch && matchesCategory
  })

  if (sortBy.value === 'price-asc') result.sort((a, b) => a.price - b.price)
  if (sortBy.value === 'price-desc') result.sort((a, b) => b.price - a.price)
  
  return result
})

// Modal & Form Logic
const showModal = ref(false)
const isEditing = ref(false)
const form = ref({ id: null, name: '', category: 'Electronics', price: 0, stock: 0, image: '' })

function openModal(product = null) {
  if (product) {
    isEditing.value = true
    form.value = { ...product }
  } else {
    isEditing.value = false
    form.value = { id: Date.now(), name: '', category: 'Electronics', price: 0, stock: 0, image: '' }
  }
  showModal.value = true
}

function handleSave() {
  const status = form.value.stock > 10 ? 'Active' : form.value.stock > 0 ? 'Low' : 'Out'
  const productData = { ...form.value, status }
  
  if (isEditing.value) {
    const index = products.value.findIndex(p => p.id === form.value.id)
    if (index !== -1) products.value[index] = productData
  } else {
    products.value.unshift(productData)
  }
  saveToStorage()
  showModal.value = false
}

function deleteProduct(id) {
  if (confirm('Are you sure you want to delete this product?')) {
    products.value = products.value.filter(p => p.id !== id)
    saveToStorage()
  }
}

function handleFileUpload(event) {
  const file = event.target.files[0]
  if (file) {
    const reader = new FileReader()
    reader.onload = (e) => {
      form.value.image = e.target.result
    }
    reader.readAsDataURL(file)
  }
}
</script>

<style scoped>
.products-page { display: flex; flex-direction: column; gap: 24px; }
.page-header { display: flex; justify-content: space-between; align-items: center; }
.title h2 { font-size: 1.75rem; font-weight: 700; margin-bottom: 4px; }
.title p { color: var(--text-muted); font-size: 0.9rem; }

.add-btn {
  background: var(--accent);
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 12px;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  box-shadow: 0 4px 15px var(--accent-glow);
}

.filters { display: flex; flex-direction: column; gap: 20px; padding: 20px 24px; }
.search-box { display: flex; align-items: center; gap: 12px; background: rgba(0, 0, 0, 0.03); border: 1px solid var(--border); padding: 10px 16px; border-radius: 12px; }
@media (prefers-color-scheme: dark) { .search-box { background: rgba(255, 255, 255, 0.05); } }
.search-box input { background: transparent; border: none; color: var(--text-main); outline: none; width: 100%; }

.filter-actions { display: flex; justify-content: space-between; align-items: center; }
.category-pills { display: flex; gap: 10px; }
.pill { background: transparent; border: 1px solid var(--border); color: var(--text-muted); padding: 6px 16px; border-radius: 20px; font-size: 0.85rem; font-weight: 500; cursor: pointer; }
.pill.active { background: var(--accent); color: white; border-color: var(--accent); }

.sort-select { background: rgba(0, 0, 0, 0.03); border: 1px solid var(--border); color: var(--text-main); padding: 8px 16px; border-radius: 10px; outline: none; }
@media (prefers-color-scheme: dark) { .sort-select { background: rgba(255, 255, 255, 0.05); } }

.products-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 24px; }

/* Form Styles */
.form-group { margin-bottom: 16px; display: flex; flex-direction: column; gap: 8px; }
.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
label { font-size: 0.9rem; font-weight: 600; color: var(--text-muted); }
input, select { background: rgba(0, 0, 0, 0.03); border: 1px solid var(--border); color: var(--text-main); padding: 12px; border-radius: 10px; outline: none; }
@media (prefers-color-scheme: dark) { input, select { background: rgba(255, 255, 255, 0.05); } }

.upload-area {
  border: 2px dashed var(--border);
  border-radius: 12px;
  height: 150px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  overflow: hidden;
}
.preview-img { width: 100%; height: 100%; object-fit: cover; }
.upload-placeholder { display: flex; flex-direction: column; align-items: center; gap: 8px; color: var(--text-muted); }
</style>

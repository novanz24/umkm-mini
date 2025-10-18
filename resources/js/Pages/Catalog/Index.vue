<script setup>
import { router, Link } from '@inertiajs/vue3'
import Pagination from '@/Components/Pagination.vue'

const props = defineProps({
  products: Object,
  categories: Array,
  filters: Object
})

const submit = (e) => {
  const params = new URLSearchParams(new FormData(e.target))
  router.get('/', Object.fromEntries(params), { preserveScroll: true, preserveState: true })
}
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-slate-50 via-blue-50 to-indigo-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <div class="mb-8 animate-fade-in-down">
        <h1 class="text-4xl font-bold bg-gradient-to-r from-blue-600 to-indigo-600 bg-clip-text text-transparent mb-2">
          Katalog Produk
        </h1>
        <p class="text-gray-600">Temukan produk terbaik untuk kebutuhan Anda</p>
      </div>

      <form @submit.prevent="submit" 
            class="bg-white/80 backdrop-blur-lg rounded-2xl shadow-xl p-6 mb-8 border border-white/20 animate-fade-in-up">
        <div class="flex flex-col sm:flex-row gap-3">
          <div class="flex-1 relative group">
            <input 
              class="w-full border-2 border-gray-200 rounded-xl px-4 py-3 pl-11 transition-all duration-300 focus:border-blue-500 focus:ring-4 focus:ring-blue-100 focus:outline-none hover:border-gray-300" 
              name="q" 
              :value="filters?.q" 
              placeholder="Cari produk..." 
            />
            <svg class="absolute left-3 top-1/2 -translate-y-1/2 w-5 h-5 text-gray-400 group-focus-within:text-blue-500 transition-colors" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
            </svg>
          </div>
          
          <select 
            class="border-2 border-gray-200 rounded-xl px-4 py-3 transition-all duration-300 focus:border-blue-500 focus:ring-4 focus:ring-blue-100 focus:outline-none hover:border-gray-300 bg-white" 
            name="category_id" 
            :value="filters?.category_id"
          >
            <option value="">Semua kategori</option>
            <option v-for="c in categories" :key="c.id" :value="c.id">{{ c.name }}</option>
          </select>
          
          <button 
            class="bg-gradient-to-r from-blue-600 to-indigo-600 text-white px-8 py-3 rounded-xl font-semibold shadow-lg hover:shadow-xl transform hover:-translate-y-0.5 active:translate-y-0 transition-all duration-200 hover:from-blue-700 hover:to-indigo-700"
          >
            Cari
          </button>
        </div>
      </form>

      <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <div 
          v-for="(p, idx) in products.data" 
          :key="p.id" 
          class="group bg-white rounded-2xl shadow-lg hover:shadow-2xl transition-all duration-300 overflow-hidden border border-gray-100 animate-fade-in-up hover:-translate-y-2"
          :style="{ animationDelay: `${idx * 50}ms` }"
        >
          <div class="h-48 bg-gradient-to-br from-blue-400 via-indigo-500 to-purple-600 relative overflow-hidden">
            <div class="absolute inset-0 bg-black/0 group-hover:bg-black/10 transition-all duration-300"></div>
            <div class="absolute inset-0 flex items-center justify-center">
              <svg class="w-20 h-20 text-white/20 group-hover:text-white/30 transition-colors duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" />
              </svg>
            </div>
          </div>
          
          <div class="p-5">
            <h3 class="font-bold text-lg mb-2 text-gray-800 group-hover:text-blue-600 transition-colors line-clamp-2">
              {{ p.name }}
            </h3>
            <div class="flex items-baseline gap-2 mb-4">
              <span class="text-2xl font-bold bg-gradient-to-r from-blue-600 to-indigo-600 bg-clip-text text-transparent">
                Rp {{ Number(p.price).toLocaleString() }}
              </span>
            </div>
            <Link 
              :href="`/products/${p.id}`" 
              class="block w-full text-center bg-gradient-to-r from-blue-50 to-indigo-50 text-blue-600 font-semibold py-3 rounded-xl hover:from-blue-600 hover:to-indigo-600 hover:text-white transition-all duration-300 transform hover:scale-105 active:scale-95"
            >
              Lihat Detail
            </Link>
          </div>
        </div>
      </div>

      <div class="mt-12">
        <Pagination :links="products.links" />
      </div>
    </div>
  </div>
</template>

<style scoped>
@keyframes fade-in-down {
  from { opacity: 0; transform: translateY(-20px); }
  to { opacity: 1; transform: translateY(0); }
}
@keyframes fade-in-up {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-fade-in-down { animation: fade-in-down 0.6s ease-out; }
.animate-fade-in-up { animation: fade-in-up 0.6s ease-out; animation-fill-mode: both; }
.line-clamp-2 { display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; }
</style>
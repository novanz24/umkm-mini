<script setup>
defineProps({ orders: Object })

const statusColors = {
  pending: 'from-yellow-100 to-amber-100 text-yellow-700',
  processing: 'from-blue-100 to-indigo-100 text-blue-700',
  completed: 'from-green-100 to-emerald-100 text-green-700',
  cancelled: 'from-red-100 to-rose-100 text-red-700'
}
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-violet-50 via-purple-50 to-fuchsia-50 py-12">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="mb-8 animate-fade-in-down">
        <h1 class="text-4xl font-bold bg-gradient-to-r from-violet-600 to-fuchsia-600 bg-clip-text text-transparent mb-2">
          Pesanan Saya
        </h1>
        <p class="text-gray-600">Kelola dan lacak semua pesanan Anda</p>
      </div>

      <div v-if="orders.data.length === 0" class="bg-white/80 backdrop-blur-lg rounded-3xl shadow-2xl p-12 border border-white/20 text-center animate-fade-in-up">
        <div class="w-32 h-32 mx-auto mb-6 bg-gradient-to-br from-violet-100 to-fuchsia-100 rounded-full flex items-center justify-center">
          <svg class="w-16 h-16 text-violet-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
          </svg>
        </div>
        <h3 class="text-2xl font-bold text-gray-800 mb-3">Belum Ada Pesanan</h3>
        <p class="text-gray-600 mb-6">Anda belum memiliki riwayat pesanan</p>
        <a 
          href="/" 
          class="inline-flex items-center gap-2 bg-gradient-to-r from-violet-600 to-fuchsia-600 text-white px-8 py-4 rounded-xl font-semibold shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 active:translate-y-0"
        >
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" />
          </svg>
          Mulai Belanja
        </a>
      </div>

      <div v-else class="space-y-4">
        <div 
          v-for="(o, idx) in orders.data" 
          :key="o.id"
          class="group bg-white/80 backdrop-blur-lg rounded-2xl shadow-lg hover:shadow-2xl border border-white/20 overflow-hidden transition-all duration-300 hover:-translate-y-1 animate-fade-in-up"
          :style="{ animationDelay: `${idx * 100}ms` }"
        >
          <div class="p-6">
            <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
              <div class="flex items-start gap-4 flex-1">
                <div class="w-16 h-16 bg-gradient-to-br from-violet-500 to-fuchsia-600 rounded-xl flex items-center justify-center flex-shrink-0 shadow-lg group-hover:scale-110 transition-transform duration-300">
                  <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                  </svg>
                </div>
                
                <div class="flex-1">
                  <div class="flex items-center gap-3 mb-2">
                    <h3 class="font-bold text-xl text-gray-800">Order #{{ o.id }}</h3>
                    <span 
                      :class="statusColors[o.status] || statusColors.pending"
                      class="px-3 py-1 rounded-full text-xs font-bold bg-gradient-to-r"
                    >
                      {{ o.status.toUpperCase() }}
                    </span>
                  </div>
                  
                  <div class="flex flex-wrap items-center gap-4 text-sm text-gray-600">
                    <div class="flex items-center gap-1">
                      <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                      </svg>
                      {{ o.created_at }}
                    </div>
                    <div class="flex items-center gap-1">
                      <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" />
                      </svg>
                      {{ o.items_count }} item
                    </div>
                  </div>
                </div>
              </div>

              <div class="flex md:flex-col items-center md:items-end gap-4 md:gap-3">
                <div class="text-right flex-1 md:flex-none">
                  <p class="text-sm text-gray-600 mb-1">Total</p>
                  <p class="text-2xl font-bold bg-gradient-to-r from-violet-600 to-fuchsia-600 bg-clip-text text-transparent">
                    Rp {{ Number(o.total).toLocaleString() }}
                  </p>
                </div>
                <a 
                  :href="`/orders/${o.id}`" 
                  class="inline-flex items-center gap-2 bg-gradient-to-r from-violet-600 to-fuchsia-600 text-white px-6 py-3 rounded-xl font-semibold shadow-lg hover:shadow-xl transition-all duration-300 transform hover:scale-105 active:scale-95"
                >
                  <span>Detail</span>
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                  </svg>
                </a>
              </div>
            </div>
          </div>
        </div>

        <div class="flex justify-center gap-3 mt-8 animate-fade-in-up" style="animation-delay: 0.3s">
          <a 
            v-if="orders.prev_page_url" 
            :href="orders.prev_page_url" 
            class="flex items-center gap-2 px-6 py-3 bg-white/80 backdrop-blur-lg border-2 border-violet-200 rounded-xl font-semibold text-violet-600 hover:bg-gradient-to-r hover:from-violet-600 hover:to-fuchsia-600 hover:text-white hover:border-transparent transition-all duration-300 shadow-lg hover:shadow-xl transform hover:-translate-y-0.5"
          >
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
            </svg>
            Sebelumnya
          </a>
          <a 
            v-if="orders.next_page_url" 
            :href="orders.next_page_url" 
            class="flex items-center gap-2 px-6 py-3 bg-white/80 backdrop-blur-lg border-2 border-violet-200 rounded-xl font-semibold text-violet-600 hover:bg-gradient-to-r hover:from-violet-600 hover:to-fuchsia-600 hover:text-white hover:border-transparent transition-all duration-300 shadow-lg hover:shadow-xl transform hover:-translate-y-0.5"
          >
            Berikutnya
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
            </svg>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@keyframes fade-in-down { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
@keyframes fade-in-up { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
.animate-fade-in-down { animation: fade-in-down 0.6s ease-out; }
.animate-fade-in-up { animation: fade-in-up 0.6s ease-out; animation-fill-mode: both; }
</style>
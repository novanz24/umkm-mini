<script setup>
const props = defineProps({
  items: { type: Array, default: () => [] },
  total: { type: Number, default: 0 },
})
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-emerald-50 via-teal-50 to-cyan-50 py-12">
    <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="mb-8 animate-fade-in-down">
        <h2 class="text-4xl font-bold bg-gradient-to-r from-emerald-600 to-teal-600 bg-clip-text text-transparent mb-2">
          Keranjang Belanja
        </h2>
        <p class="text-gray-600">{{ props.items.length }} item dalam keranjang</p>
      </div>

      <template v-if="props.items.length">
        <div class="bg-white/80 backdrop-blur-lg rounded-3xl shadow-2xl overflow-hidden border border-white/20 mb-6 animate-fade-in-up">
          <div class="overflow-x-auto">
            <table class="w-full">
              <thead>
                <tr class="bg-gradient-to-r from-emerald-500 to-teal-500 text-white">
                  <th class="px-6 py-4 text-left font-semibold rounded-tl-3xl">Produk</th>
                  <th class="px-6 py-4 text-center font-semibold">Jumlah</th>
                  <th class="px-6 py-4 text-right font-semibold">Harga</th>
                  <th class="px-6 py-4 text-right font-semibold rounded-tr-3xl">Subtotal</th>
                </tr>
              </thead>
              <tbody>
                <tr 
                  v-for="(i, idx) in props.items" 
                  :key="i.id" 
                  class="border-b border-gray-100 hover:bg-emerald-50/50 transition-colors duration-200 animate-slide-in"
                  :style="{ animationDelay: `${idx * 100}ms` }"
                >
                  <td class="px-6 py-5">
                    <div class="flex items-center gap-4">
                      <div class="w-16 h-16 rounded-xl bg-gradient-to-br from-emerald-400 to-teal-500 flex items-center justify-center flex-shrink-0 shadow-md">
                        <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" />
                        </svg>
                      </div>
                      <span class="font-semibold text-gray-800">{{ i.name }}</span>
                    </div>
                  </td>
                  <td class="px-6 py-5 text-center">
                    <span class="inline-flex items-center justify-center w-12 h-12 bg-gradient-to-br from-emerald-100 to-teal-100 text-emerald-700 rounded-xl font-bold">
                      {{ i.qty }}
                    </span>
                  </td>
                  <td class="px-6 py-5 text-right font-medium text-gray-700">
                    Rp {{ Number(i.price).toLocaleString() }}
                  </td>
                  <td class="px-6 py-5 text-right font-bold text-emerald-600">
                    Rp {{ Number(i.subtotal).toLocaleString() }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <div class="bg-white/80 backdrop-blur-lg rounded-3xl shadow-2xl p-8 border border-white/20 animate-fade-in-up" style="animation-delay: 0.2s">
          <div class="flex flex-col sm:flex-row items-center justify-between gap-6">
            <div>
              <p class="text-gray-600 text-sm mb-1">Total Pembayaran</p>
              <p class="text-4xl font-bold bg-gradient-to-r from-emerald-600 to-teal-600 bg-clip-text text-transparent">
                Rp {{ Number(props.total).toLocaleString() }}
              </p>
            </div>
            <a 
              href="/checkout"
              class="group relative px-8 py-4 bg-gradient-to-r from-emerald-600 to-teal-600 text-white rounded-xl font-bold shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 active:translate-y-0 flex items-center gap-3 overflow-hidden"
            >
              <span class="absolute inset-0 bg-gradient-to-r from-emerald-700 to-teal-700 opacity-0 group-hover:opacity-100 transition-opacity duration-300"></span>
              <svg class="w-6 h-6 relative z-10" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
              </svg>
              <span class="relative z-10">Lanjut ke Checkout</span>
            </a>
          </div>
        </div>
      </template>

      <template v-else>
        <div class="bg-white/80 backdrop-blur-lg rounded-3xl shadow-2xl p-12 border border-white/20 text-center animate-fade-in-up">
          <div class="w-32 h-32 mx-auto mb-6 bg-gradient-to-br from-gray-100 to-gray-200 rounded-full flex items-center justify-center">
            <svg class="w-16 h-16 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
            </svg>
          </div>
          <h3 class="text-2xl font-bold text-gray-800 mb-3">Keranjang Kosong</h3>
          <p class="text-gray-600 mb-6">Belum ada produk dalam keranjang Anda</p>
          <a 
            href="/" 
            class="inline-flex items-center gap-2 bg-gradient-to-r from-emerald-600 to-teal-600 text-white px-8 py-4 rounded-xl font-semibold shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 active:translate-y-0"
          >
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
            </svg>
            Lihat Katalog
          </a>
        </div>
      </template>
    </div>
  </div>
</template>

<style scoped>
@keyframes fade-in-down { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
@keyframes fade-in-up { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
@keyframes slide-in { from { opacity: 0; transform: translateX(-20px); } to { opacity: 1; transform: translateX(0); } }
.animate-fade-in-down { animation: fade-in-down 0.6s ease-out; }
.animate-fade-in-up { animation: fade-in-up 0.6s ease-out; animation-fill-mode: both; }
.animate-slide-in { animation: slide-in 0.5s ease-out; animation-fill-mode: both; }
</style>
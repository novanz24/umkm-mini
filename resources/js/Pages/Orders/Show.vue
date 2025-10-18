<script setup>
defineProps({ order: Object })

const statusConfig = {
  pending: {
    color: 'from-yellow-500 to-amber-500',
    bg: 'from-yellow-50 to-amber-50',
    icon: 'M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z'
  },
  processing: {
    color: 'from-blue-500 to-indigo-500',
    bg: 'from-blue-50 to-indigo-50',
    icon: 'M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15'
  },
  completed: {
    color: 'from-green-500 to-emerald-500',
    bg: 'from-green-50 to-emerald-50',
    icon: 'M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z'
  },
  cancelled: {
    color: 'from-red-500 to-rose-500',
    bg: 'from-red-50 to-rose-50',
    icon: 'M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z'
  }
}
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-rose-50 via-pink-50 to-red-50 py-12">
    <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
      <a 
        href="/orders" 
        class="inline-flex items-center gap-2 text-gray-600 hover:text-rose-600 font-semibold mb-6 transition-colors animate-fade-in"
      >
        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
        </svg>
        Kembali ke Daftar Pesanan
      </a>

      <div class="mb-8 animate-fade-in-down">
        <h1 class="text-4xl font-bold bg-gradient-to-r from-rose-600 to-pink-600 bg-clip-text text-transparent mb-2">
          Order #{{ order.id }}
        </h1>
        <p class="text-gray-600">Detail pesanan dan informasi pengiriman</p>
      </div>

      <div :class="`bg-gradient-to-r ${statusConfig[order.status]?.bg || statusConfig.pending.bg} border-2 border-white/50 rounded-3xl p-6 mb-6 shadow-xl animate-fade-in-up`">
        <div class="flex items-center gap-4">
          <div :class="`w-16 h-16 bg-gradient-to-br ${statusConfig[order.status]?.color || statusConfig.pending.color} rounded-2xl flex items-center justify-center shadow-lg`">
            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="statusConfig[order.status]?.icon || statusConfig.pending.icon" />
            </svg>
          </div>
          <div class="flex-1">
            <p class="text-sm font-semibold text-gray-700 mb-1">Status Pesanan</p>
            <p class="text-2xl font-bold capitalize" :class="`bg-gradient-to-r ${statusConfig[order.status]?.color || statusConfig.pending.color} bg-clip-text text-transparent`">
              {{ order.status }}
            </p>
          </div>
          <div class="text-right">
            <p class="text-sm text-gray-600 mb-1">Tanggal Pesanan</p>
            <p class="font-bold text-gray-800">{{ order.created_at }}</p>
          </div>
        </div>
      </div>

      <div class="grid md:grid-cols-2 gap-6 mb-6">
        <div class="bg-white/80 backdrop-blur-lg rounded-3xl shadow-xl p-6 border border-white/20 animate-fade-in-left">
          <div class="flex items-center gap-3 mb-4">
            <div class="w-12 h-12 bg-gradient-to-br from-rose-100 to-pink-100 rounded-xl flex items-center justify-center">
              <svg class="w-6 h-6 text-rose-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
            </div>
            <h2 class="text-xl font-bold text-gray-800">Alamat Pengiriman</h2>
          </div>
          <div class="bg-gray-50 rounded-xl p-4">
            <p class="text-gray-700 whitespace-pre-line leading-relaxed">{{ order.address_text }}</p>
          </div>
        </div>

        <div class="bg-white/80 backdrop-blur-lg rounded-3xl shadow-xl p-6 border border-white/20 animate-fade-in-right">
          <div class="flex items-center gap-3 mb-4">
            <div class="w-12 h-12 bg-gradient-to-br from-rose-100 to-pink-100 rounded-xl flex items-center justify-center">
              <svg class="w-6 h-6 text-rose-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
              </svg>
            </div>
            <h2 class="text-xl font-bold text-gray-800">Ringkasan</h2>
          </div>
          <div class="space-y-3">
            <div class="flex justify-between items-center py-2 border-b border-gray-200">
              <span class="text-gray-600">Total Item</span>
              <span class="font-bold text-gray-800">{{ order.items.length }}</span>
            </div>
            <div class="flex justify-between items-center py-3 bg-gradient-to-r from-rose-50 to-pink-50 rounded-xl px-4">
              <span class="text-gray-700 font-semibold">Total Pembayaran</span>
              <span class="text-2xl font-bold bg-gradient-to-r from-rose-600 to-pink-600 bg-clip-text text-transparent">
                Rp {{ Number(order.total).toLocaleString() }}
              </span>
            </div>
          </div>
        </div>
      </div>

      <div class="bg-white/80 backdrop-blur-lg rounded-3xl shadow-xl overflow-hidden border border-white/20 animate-fade-in-up" style="animation-delay: 0.2s">
        <div class="bg-gradient-to-r from-rose-500 to-pink-500 p-6">
          <h2 class="text-2xl font-bold text-white flex items-center gap-3">
            <svg class="w-7 h-7" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" />
            </svg>
            Item Pesanan
          </h2>
        </div>

        <div class="p-6">
          <div class="overflow-x-auto">
            <table class="w-full">
              <thead>
                <tr class="border-b-2 border-gray-200">
                  <th class="text-left py-4 px-2 font-bold text-gray-700">Produk</th>
                  <th class="text-center py-4 px-2 font-bold text-gray-700">Qty</th>
                  <th class="text-right py-4 px-2 font-bold text-gray-700">Harga</th>
                  <th class="text-right py-4 px-2 font-bold text-gray-700">Subtotal</th>
                </tr>
              </thead>
              <tbody>
                <tr 
                  v-for="(i, idx) in order.items" 
                  :key="i.id" 
                  class="border-b border-gray-100 hover:bg-rose-50/50 transition-colors animate-slide-in"
                  :style="{ animationDelay: `${idx * 100}ms` }"
                >
                  <td class="py-4 px-2">
                    <div class="flex items-center gap-3">
                      <div class="w-14 h-14 bg-gradient-to-br from-rose-400 to-pink-500 rounded-xl flex items-center justify-center flex-shrink-0 shadow-md">
                        <svg class="w-7 h-7 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" />
                        </svg>
                      </div>
                      <span class="font-semibold text-gray-800">{{ i.name }}</span>
                    </div>
                  </td>
                  <td class="py-4 px-2 text-center">
                    <span class="inline-flex items-center justify-center w-10 h-10 bg-gradient-to-br from-rose-100 to-pink-100 text-rose-700 rounded-lg font-bold">
                      {{ i.qty }}
                    </span>
                  </td>
                  <td class="py-4 px-2 text-right font-medium text-gray-700">
                    Rp {{ Number(i.price).toLocaleString() }}
                  </td>
                  <td class="py-4 px-2 text-right font-bold text-rose-600">
                    Rp {{ Number(i.subtotal).toLocaleString() }}
                  </td>
                </tr>
              </tbody>
              <tfoot>
                <tr class="bg-gradient-to-r from-rose-50 to-pink-50">
                  <td colspan="3" class="py-4 px-2 text-right font-bold text-gray-800 text-lg">
                    Total Pesanan
                  </td>
                  <td class="py-4 px-2 text-right text-2xl font-bold bg-gradient-to-r from-rose-600 to-pink-600 bg-clip-text text-transparent">
                    Rp {{ Number(order.total).toLocaleString() }}
                  </td>
                </tr>
              </tfoot>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@keyframes fade-in { from { opacity: 0; } to { opacity: 1; } }
@keyframes fade-in-down { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
@keyframes fade-in-up { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
@keyframes fade-in-left { from { opacity: 0; transform: translateX(-30px); } to { opacity: 1; transform: translateX(0); } }
@keyframes fade-in-right { from { opacity: 0; transform: translateX(30px); } to { opacity: 1; transform: translateX(0); } }
@keyframes slide-in { from { opacity: 0; transform: translateX(-20px); } to { opacity: 1; transform: translateX(0); } }
.animate-fade-in { animation: fade-in 0.5s ease-out; }
.animate-fade-in-down { animation: fade-in-down 0.6s ease-out; }
.animate-fade-in-up { animation: fade-in-up 0.6s ease-out; animation-fill-mode: both; }
.animate-fade-in-left { animation: fade-in-left 0.6s ease-out; }
.animate-fade-in-right { animation: fade-in-right 0.6s ease-out; }
.animate-slide-in { animation: slide-in 0.5s ease-out; animation-fill-mode: both; }
</style>
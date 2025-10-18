<script setup>
import { useForm } from '@inertiajs/vue3'
import FormError from '@/Components/FormError.vue'

const props = defineProps({ total: Number })

const form = useForm({ address_text: '' })

const submit = () => {
  if (!form.address_text || form.address_text.length < 10) {
    form.errors.address_text = 'Alamat minimal 10 karakter'
    return
  }
  form.post('/checkout')
}
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-amber-50 via-orange-50 to-red-50 py-12">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-8 animate-fade-in-down">
        <div class="inline-block p-4 bg-gradient-to-br from-amber-100 to-orange-100 rounded-full mb-4">
          <svg class="w-12 h-12 text-orange-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
        </div>
        <h2 class="text-4xl font-bold bg-gradient-to-r from-amber-600 to-orange-600 bg-clip-text text-transparent mb-2">
          Checkout
        </h2>
        <p class="text-gray-600">Lengkapi data pengiriman Anda</p>
      </div>

      <div class="bg-white/80 backdrop-blur-lg rounded-3xl shadow-2xl p-8 border border-white/20 mb-6 animate-fade-in-up">
        <div class="flex items-center justify-between pb-6 border-b border-gray-200">
          <span class="text-gray-600 font-medium">Total Pembayaran</span>
          <span class="text-3xl font-bold bg-gradient-to-r from-amber-600 to-orange-600 bg-clip-text text-transparent">
            Rp {{ Number(total).toLocaleString() }}
          </span>
        </div>
      </div>

      <form @submit.prevent="submit" class="bg-white/80 backdrop-blur-lg rounded-3xl shadow-2xl p-8 border border-white/20 space-y-6 animate-fade-in-up" style="animation-delay: 0.1s">
        <div>
          <label class="block text-sm font-bold text-gray-700 mb-3 flex items-center gap-2">
            <svg class="w-5 h-5 text-orange-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
            </svg>
            Alamat Pengiriman Lengkap
          </label>
          <textarea 
            v-model.trim="form.address_text" 
            required 
            rows="5"
            class="w-full border-2 border-gray-200 rounded-2xl p-4 transition-all duration-300 focus:border-orange-500 focus:ring-4 focus:ring-orange-100 focus:outline-none hover:border-gray-300 resize-none"
            placeholder="Masukkan alamat lengkap termasuk nama jalan, nomor rumah, RT/RW, kelurahan, kecamatan, kota, dan kode pos..."
          ></textarea>
          <FormError :msg="form.errors.address_text" />
        </div>

        <button 
          type="submit"
          class="w-full bg-gradient-to-r from-amber-600 to-orange-600 text-white font-bold py-4 px-6 rounded-2xl shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 active:translate-y-0 disabled:opacity-50 disabled:cursor-not-allowed disabled:transform-none flex items-center justify-center gap-3 group"
          :disabled="form.processing"
        >
          <svg class="w-6 h-6 group-hover:scale-110 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
          </svg>
          <span>{{ form.processing ? 'Memproses...' : 'Buat Pesanan' }}</span>
        </button>

        <div class="flex items-center gap-3 p-4 bg-gradient-to-r from-blue-50 to-indigo-50 rounded-xl border border-blue-100">
          <svg class="w-6 h-6 text-blue-600 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
          </svg>
          <p class="text-sm text-blue-700">
            <span class="font-semibold">Transaksi Aman</span> - Data Anda dilindungi dengan enkripsi
          </p>
        </div>
      </form>

      <div 
        v-if="$page.props.flash?.ok" 
        class="mt-6 bg-gradient-to-r from-green-50 to-emerald-50 border-2 border-green-200 rounded-2xl p-6 animate-bounce-in"
      >
        <div class="flex items-center gap-4">
          <div class="w-12 h-12 bg-gradient-to-br from-green-500 to-emerald-500 rounded-full flex items-center justify-center flex-shrink-0">
            <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
            </svg>
          </div>
          <div>
            <p class="font-bold text-green-800 text-lg">Pesanan Berhasil!</p>
            <p class="text-green-700">{{ $page.props.flash.ok }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@keyframes fade-in-down { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
@keyframes fade-in-up { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
@keyframes bounce-in { 0% { opacity: 0; transform: scale(0.3); } 50% { transform: scale(1.05); } 70% { transform: scale(0.9); } 100% { opacity: 1; transform: scale(1); } }
.animate-fade-in-down { animation: fade-in-down 0.6s ease-out; }
.animate-fade-in-up { animation: fade-in-up 0.6s ease-out; animation-fill-mode: both; }
.animate-bounce-in { animation: bounce-in 0.5s ease-out; }
</style>
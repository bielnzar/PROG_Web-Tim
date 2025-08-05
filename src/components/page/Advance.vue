<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-50 p-4 mt-20">
    <h2
      data-aos="fade-down"
      class="place-self-center lg:text-7xl font-bold leading-tight md:text-6xl sm:text-6xl md:mt-0 text-5xl gradient-text"
    >
      Road to Advance 1.0
    </h2>
    <h4 class="text-center text-xl italic text-gray-500 mt-4 mb-8 max-w-3xl" data-aos="zoom-in">“Discover. Learn. Build. Your Robotic Foundation Begins Here”</h4>
    <div class="w-full max-w-2xl p-8 space-y-6 mt-10 bg-white rounded-xl shadow-2xl mb-30">
      <h1 class="text-3xl font-bold text-center text-gray-900">Workshop Registration Form</h1>
      
      <form 
        @submit.prevent="handleSubmit"
        class="space-y-6"
      >
        <div v-if="message" :class="isError ? 'bg-red-100 border-red-400 text-red-700' : 'bg-green-100 border-green-400 text-green-700'" class="border px-4 py-3 rounded-md" role="alert">
          <p class="font-bold">{{ isError ? 'Terjadi Kesalahan' : 'Berhasil!' }}</p>
          <p class="text-sm">{{ message }}</p>
        </div>

        <div>
          <label for="Nama" class="block text-sm font-medium text-gray-700">Nama Lengkap</label>
          <input 
            v-model="formData.Nama"
            id="Nama"
            name="Nama" 
            type="text" 
            placeholder="Masukkan nama lengkap Anda" 
            required
            class="w-full px-4 py-2 mt-2 text-gray-900 bg-gray-50 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-red-500"
          >
        </div>

        <div>
          <label for="NRP" class="block text-sm font-medium text-gray-700">NRP / NIM</label>
          <input 
            v-model="formData.NRP"
            id="NRP"
            name="NRP" 
            type="text" 
            placeholder="Masukkan NRP atau NIM Anda" 
            required
            class="w-full px-4 py-2 mt-2 text-gray-900 bg-gray-50 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-red-500"
          >
        </div>
        
        <div>
          <label for="Asal-Universitas" class="block text-sm font-medium text-gray-700">Asal Universitas</label>
          <input 
            v-model="formData['Asal Universitas']"
            id="Asal-Universitas"
            name="Asal Universitas" 
            type="text" 
            placeholder="Contoh: Institut Teknologi Sepuluh Nopember" 
            required
            class="w-full px-4 py-2 mt-2 text-gray-900 bg-gray-50 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-red-500"
          >
        </div>

        <div>
          <label for="Departemen" class="block text-sm font-medium text-gray-700">Departemen / Jurusan</label>
          <input 
            v-model="formData.Departemen"
            id="Departemen"
            name="Departemen" 
            type="text" 
            placeholder="Contoh: Teknik Informatika" 
            required
            class="w-full px-4 py-2 mt-2 text-gray-900 bg-gray-50 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-red-500"
          >
        </div>

        <div>
          <label for="No-WA" class="block text-sm font-medium text-gray-700">No. WA</label>
          <input 
            v-model="formData['No. WA']"
            id="No-WA"
            name="No. WA" 
            type="tel" 
            placeholder="Contoh: 085781821926" 
            required
            class="w-full px-4 py-2 mt-2 text-gray-900 bg-gray-50 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-red-500"
          >
        </div>

        <div>
          <label for="Email" class="block text-sm font-medium text-gray-700">Email</label>
          <input 
            v-model="formData.Email"
            id="Email"
            name="Email" 
            type="email" 
            placeholder="Contoh: example@gmail.com" 
            required
            class="w-full px-4 py-2 mt-2 text-gray-900 bg-gray-50 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-red-500"
          >
        </div>

        <div>
          <label for="Paket-Pilihan" class="block text-sm font-medium text-gray-700">Paket Pilihan</label>
          <select 
            v-model="formData['Paket Pilihan']"
            id="Paket-Pilihan"
            name="Paket Pilihan" 
            required
            class="w-full px-4 py-2 mt-2 text-gray-900 bg-gray-50 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-red-500"
          >
            <option value="" disabled>-- Pilih salah satu paket --</option>
            <option value="Paket A - Materi & Sertifikat">Paket A - Materi & Sertifikat</option>
            <option value="Paket B - Materi, Sertifikat & Merchandise">Paket B - Materi, Sertifikat & Merchandise</option>
            <option value="Paket C - Full Access">Paket C - Full Access</option>
          </select>
        </div>

        <button 
          type="submit"
          :disabled="isLoading"
          class="w-full mt-6 px-4 py-3 font-semibold text-xl text-white bg-red-600 rounded-md hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500 transition-colors duration-300 disabled:bg-red-400 disabled:cursor-not-allowed"
        >
          {{ isLoading ? 'Mengirim...' : 'Yok di Submit!' }}
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';

const scriptURL = 'https://script.google.com/macros/s/AKfycbz_6b_eyP2DeFiwXF_WqQQPK2f2LHm6pRXbCVUFJCYbo7amwJyVlTo8SThmUfL0X_NjFA/exec';

const formData = reactive({
  'Nama': '',
  'NRP': '',
  'Asal Universitas': '',
  'Departemen': '',
  'No. WA': '',
  'Email': '',
  'Paket Pilihan': '',
});

const isLoading = ref(false);
const message = ref('');
const isError = ref(false);

const handleSubmit = async () => {
  isLoading.value = true;
  message.value = '';
  isError.value = false;

  const body = new FormData();
  for (const key in formData) {
      body.append(key, formData[key]);
  }

  try {
    const response = await fetch(scriptURL, { method: 'POST', body: body });
    const result = await response.json();

    if (result.result === 'success') {
      message.value = 'Data Anda telah berhasil terkirim. Terima kasih!';
      isError.value = false;
      Object.keys(formData).forEach(key => {
        formData[key] = '';
      });
    } else {
      throw new Error(result.error || 'Terjadi kesalahan yang tidak diketahui.');
    }
  } catch (error) {
    message.value = `Gagal mengirim data: ${error.message}`;
    isError.value = true;
  } finally {
    isLoading.value = false;
  }
};
</script>

<style scoped>

</style>
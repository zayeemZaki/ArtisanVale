<template>
  <div
    class="space-y-4 w-full p-6 rounded-2xl shadow-xl bg-white/60 backdrop-blur-md border border-white/30 transition-all duration-300"
  >
    <!-- Brand Name -->
    <input
      type="text"
      placeholder="✨ Brand Name (e.g., GlowSkin Co.)"
      class="w-full px-5 py-3 rounded-lg border border-gray-200 shadow-inner bg-white/50 placeholder:text-pink-400 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-300 focus:border-transparent transition duration-200"
      v-model="localBrandName"
      @input="$emit('update:brandName', localBrandName)"
    />

    <!-- Product Name -->
    <input
      type="text"
      placeholder="💧 Product Name (e.g., Vitamin C Serum)"
      class="w-full px-5 py-3 rounded-lg border border-gray-200 shadow-inner bg-white/50 placeholder:text-pink-400 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-300 focus:border-transparent transition duration-200"
      v-model="localProductName"
      @input="$emit('update:productName', localProductName)"
    />

    <!-- Image URL -->
    <input
      type="url"
      placeholder="🌸 Paste image URL (optional)"
      class="w-full px-5 py-3 rounded-lg border border-gray-200 shadow-inner bg-white/50 placeholder:text-pink-400 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-300 focus:border-transparent transition duration-200"
      v-model="localImageUrl"
      @input="$emit('update:imageUrl', localImageUrl)"
    />

    <!-- Animated Preview -->
    <transition name="fade">
      <div v-if="localImageUrl" class="mt-2 rounded-lg overflow-hidden border border-gray-200 shadow-md">
        <img
          :src="localImageUrl"
          alt="Product preview"
          class="w-full h-auto object-cover"
        />
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  brandName: String,
  productName: String,
  imageUrl: String
})

const localBrandName = ref(props.brandName || '')
const localProductName = ref(props.productName || '')
const localImageUrl = ref(props.imageUrl || '')

// Keep inputs in sync with parent updates
watch(() => props.brandName, val => (localBrandName.value = val))
watch(() => props.productName, val => (localProductName.value = val))
watch(() => props.imageUrl, val => (localImageUrl.value = val))
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

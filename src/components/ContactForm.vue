<template>
  <form
    class="space-y-4 w-full p-6 rounded-2xl shadow-xl bg-white/60 backdrop-blur-md border border-white/30 transition-all duration-300 max-w-md mx-auto"
  >
    <!-- Name -->
    <input
      type="text"
      id="name"
      :value="name"
      @input="$emit('update:name', $event.target.value)"
      placeholder="🧑 Your Name (e.g., Zayeem Zaki)"
      autocomplete="name"
      class="w-full px-5 py-3 rounded-lg border border-gray-200 shadow-inner bg-white/50 placeholder:text-pink-400 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-300 focus:border-transparent transition duration-200"
    />

    <!-- Email -->
    <input
      type="email"
      id="email"
      :value="email"
      @input="$emit('update:email', $event.target.value)"
      placeholder="✉️ Email Address (e.g., artisanvale@gmail.com)"
      autocomplete="email"
      class="w-full px-5 py-3 rounded-lg border border-gray-200 shadow-inner bg-white/50 placeholder:text-pink-400 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-300 focus:border-transparent transition duration-200"
    />

    <!-- Phone -->
    <input
      type="tel"
      id="phone"
      :value="phone"
      @input="$emit('update:phone', $event.target.value)"
      placeholder="📱 Phone Number (optional)"
      autocomplete="tel"
      class="w-full px-5 py-3 rounded-lg border border-gray-200 shadow-inner bg-white/50 placeholder:text-pink-400 text-gray-800 focus:outline-none focus:ring-2 focus:ring-pink-300 focus:border-transparent transition duration-200"
    />
  </form>
</template>

<script setup>
defineProps({
  name: String,
  email: String,
  phone: String
});
defineEmits(['update:name', 'update:email', 'update:phone']);
</script>

<style scoped>
input:-webkit-autofill {
  box-shadow: 0 0 0px 1000px rgba(255, 255, 255, 0.6) inset !important;
  -webkit-box-shadow: 0 0 0px 1000px rgba(255, 255, 255, 0.6) inset !important;
  border-radius: 0.75rem;
  padding-left: 1rem !important;
  padding-right: 1rem !important;
}
</style>

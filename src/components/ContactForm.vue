<template>
  <form class="space-y-4 w-full max-w-md mx-auto px-4 sm:px-8">
    <div>
      <label for="name" class="block text-sm font-semibold text-gray-700 mb-1">Your Name</label>
      <input
        type="text"
        id="name"
        :value="name"
        @input="$emit('update:name', $event.target.value)"
        placeholder="Enter your name"
        autocomplete="name"
        class="w-full bg-white/60 backdrop-blur-md border border-gray-300 text-sm rounded-xl px-4 py-3 shadow-inner focus:outline-none focus:ring-2 focus:ring-pink-400 transition"
      />
    </div>

    <div>
      <label for="email" class="block text-sm font-semibold text-gray-700 mb-1">Email Address</label>
      <input
        type="email"
        id="email"
        :value="email"
        @input="$emit('update:email', $event.target.value)"
        placeholder="Enter your email"
        autocomplete="email"
        class="w-full bg-white/60 backdrop-blur-md border border-gray-300 text-sm rounded-xl px-4 py-3 shadow-inner focus:outline-none focus:ring-2 focus:ring-pink-400 transition"
      />
    </div>

    <div>
      <label for="phone" class="block text-sm font-semibold text-gray-700 mb-1">Phone Number (optional)</label>
      <input
        type="tel"
        id="phone"
        :value="phone"
        @input="$emit('update:phone', $event.target.value)"
        placeholder="Enter your phone number"
        autocomplete="tel"
        class="w-full bg-white/60 backdrop-blur-md border border-pink-300 text-sm rounded-xl px-4 py-3 shadow-inner focus:outline-none focus:ring-2 focus:ring-pink-400 transition"
      />
    </div>
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

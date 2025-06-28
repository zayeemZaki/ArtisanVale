<template>
  <div
    :class="[
      sender === 'bot'
        ? 'bg-pink-100 text-pink-800 self-start'
        : 'bg-blue-100 text-blue-900 self-end',
      'rounded-xl px-6 py-4 max-w-[95%] w-fit shadow-lg text-base sm:text-xl font-semibold leading-relaxed mt-4 mb-2 mx-auto text-center'
    ]"
  >
    <slot />
  </div>
</template>

<script setup>
defineProps({
  sender: {
    type: String,
    default: 'bot'
  }
});
</script>

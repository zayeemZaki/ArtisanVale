<template>
  <div
    :class="[
      sender === 'bot'
        ? 'bg-pink-100 text-pink-900 self-start'
        : 'bg-blue-100 text-blue-900 self-end',
      'rounded-full px-6 py-3 max-w-[95%] w-fit shadow-md text-base sm:text-lg leading-relaxed mt-4 mb-2 mx-auto'
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

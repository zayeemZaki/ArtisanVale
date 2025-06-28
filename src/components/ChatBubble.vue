<template>
  <div
    :class="[
      sender === 'bot' ? 'bg-pink-100 text-pink-800 self-start' : 'bg-blue-100 text-blue-800 self-end',
      'rounded-xl px-4 py-2 w-fit max-w-[85%]'
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

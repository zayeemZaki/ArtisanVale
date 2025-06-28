<template>
  <div class="space-y-3">
    <input
      type="text"
      :value="name"
      @input="$emit('update:name', $event.target.value)"
      placeholder="Your name"
      class="w-full px-3 py-2 border border-gray-300 rounded text-sm"
    />

    <input
      type="email"
      :value="email"
      @input="$emit('update:email', $event.target.value)"
      placeholder="Your email"
      class="w-full px-3 py-2 border border-gray-300 rounded text-sm"
    />

    <input
      type="tel"
      :value="phone"
      @input="$emit('update:phone', $event.target.value)"
      placeholder="Phone (optional)"
      class="w-full px-3 py-2 border border-gray-300 rounded text-sm"
    />
  </div>
</template>

<script>
export default {
  props: ['name', 'email', 'phone'],
  emits: ['update:name', 'update:email', 'update:phone']
};
</script>

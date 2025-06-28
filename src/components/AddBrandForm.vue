<template>
  <div class="space-y-3">
    <input
      type="text"
      :value="brandName"
      @input="$emit('update:brandName', $event.target.value)"
      class="w-full px-3 py-2 border border-gray-300 rounded text-sm"
      placeholder="Brand name (optional)"
    />

    <input
      type="text"
      :value="productName"
      @input="$emit('update:productName', $event.target.value)"
      class="w-full px-3 py-2 border border-gray-300 rounded text-sm"
      placeholder="Product name (optional)"
    />

    <input
      type="file"
      class="w-full px-3 py-2 border border-gray-300 rounded text-sm"
      @change="handleImageUpload"
    />
  </div>
</template>

<script>
export default {
  props: ['brandName', 'productName', 'imageData'],
  emits: ['update:brandName', 'update:productName', 'update:imageData'],
  methods: {
    handleImageUpload(event) {
      const file = event.target.files[0];
      if (!file) return;

      const reader = new FileReader();
      reader.onload = () => {
        this.$emit('update:imageData', reader.result);
      };
      reader.readAsDataURL(file);
    }
  }
};
</script>

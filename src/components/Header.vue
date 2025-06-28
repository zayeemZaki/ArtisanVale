<template>
  <header
    class="w-full px-6 pt-4 pb-4 flex flex-col sm:flex-row sm:justify-between sm:items-start sm:gap-6 bg-transparent text-center sm:text-left"
  >
    <!-- Tagline: Top on mobile, right on desktop -->
    <div class="order-1 sm:order-2 mb-2 sm:mb-0 sm:self-start sm:pt-1">
      <span
        class="shimmer-badge hover:shadow-md hover:scale-105 transition-transform duration-300"
      >
        ✨ Shaping our collection — <strong>with your voice</strong>
      </span>
    </div>

    <!-- Logo: Below tagline on mobile, left on desktop -->
    <div class="order-2 sm:order-1 flex justify-center sm:justify-start">
      <img
        src="/ArtisanVale.png"
        alt="ArtisanVale Logo"
        class="h-24 w-48 sm:h-28 sm:w-56 object-contain rounded-2xl border border-gray-300 shadow-md bg-white p-1"
      />
    </div>
  </header>
</template>

<script setup>
// No logic needed
</script>

<style>
.shimmer-badge {
  position: relative;
  display: inline-block;
  padding: 0.5rem 1rem;
  border-radius: 9999px;
  font-weight: 500;
  font-size: 0.875rem;
  background: linear-gradient(to right, #fce7f3, #fecdd3);
  color: #be185d;
  overflow: hidden;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.06);
  transition: all 0.3s ease;
}

.shimmer-badge::before {
  content: "";
  position: absolute;
  top: 0;
  left: -50%;
  width: 200%;
  height: 100%;
  background: linear-gradient(
    120deg,
    transparent,
    rgba(255, 255, 255, 0.6),
    transparent
  );
  animation: shimmer-swipe 2s infinite;
  z-index: 1;
}

@keyframes shimmer-swipe {
  0% {
    left: -100%;
  }
  100% {
    left: 100%;
  }
}
</style>

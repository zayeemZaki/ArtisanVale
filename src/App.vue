<template>
  <div class="h-full bg-[#fcfbf5] flex flex-col relative">
    <!-- Splash Screen -->
    <div
      v-if="showSplash"
      class="fixed inset-0 z-50 flex items-center justify-center bg-[#fcfbf5] text-center px-4"
    >
      <div>
        <h1 class="text-2xl sm:text-3xl font-semibold text-pink-600 animate-pulse">
          Welcome to ArtisanVale 💖
        </h1>
        <p class="mt-2 text-gray-700 text-sm">
          Your voice shapes our skincare collection — founded by Zayeem.
        </p>
      </div>
    </div>

    <!-- Fixed Header -->
    <div
      class="fixed top-0 left-0 right-0 z-40 bg-white/70 backdrop-blur-md border-b border-pink-100 shadow"
    >
      <Header />
    </div>

    <!-- Main Content -->
    <main
      v-show="!showSplash"
      class="flex-1 max-w-md w-full mx-auto px-4 pt-[180px] pb-[72px] overflow-hidden relative"
    >
      <ConversationalForm />
    </main>

    <!-- Fixed Footer -->
    <div
      v-show="!showSplash"
      class="fixed bottom-0 left-0 right-0 z-40 bg-white/80 backdrop-blur-md h-[72px]"
    >
      <Footer />
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
import ConversationalForm from './components/ConversationalForm.vue';

export default {
  components: {
    Header,
    Footer,
    ConversationalForm
  },
  setup() {
    const showSplash = ref(true);

    onMounted(() => {
      setTimeout(() => {
        showSplash.value = false;
      }, 2200); // ~2.2 seconds splash duration
    });

    return {
      showSplash
    };
  }
};
</script>

<style>
html,
body,
#app {
  height: 100%;
  overflow: hidden;
}
</style>

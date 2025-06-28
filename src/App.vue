<template>
  <div class="h-full bg-[#fcfbf5] flex flex-col">
    <!-- Fixed Header -->
    <div
      class="fixed top-0 left-0 right-0 z-50 bg-white/70 backdrop-blur-md border-b border-pink-100 shadow"
    >
      <Header />
    </div>

    <!-- Main Content -->
<main class="flex-1 max-w-md w-full mx-auto px-4 pt-[180px] pb-[72px] overflow-hidden relative">
      <ConversationalForm />
    </main>

    <!-- Fixed Footer -->
    <div
      class="fixed bottom-0 left-0 right-0 z-50 bg-white/80 backdrop-blur-md h-[72px]"
    >
      <Footer />
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
import ConversationalForm from './components/ConversationalForm.vue';

export default {
  components: {
    Header,
    Footer,
    ConversationalForm
  }
};
</script>



<style>
html, body, #app {
  height: 100%;
  overflow: hidden;
}

</style>

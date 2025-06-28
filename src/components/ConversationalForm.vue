<template>
  <div class="flex flex-col space-y-4 text-sm sm:text-base text-gray-800">
    <!-- Step 1 -->
    <div v-if="step === 1" class="flex flex-col space-y-2">
      <ChatBubble sender="bot">Hey there! 👋 Which skincare brands do you love?</ChatBubble>
      <BrandList :selectedBrands="selectedBrands" @update:selectedBrands="selectedBrands = $event" />
      <div class="flex justify-end w-full">
        <button
          class="mt-2 bg-pink-500 hover:bg-pink-600 text-white font-medium px-5 py-2 rounded-full shadow transition-all duration-200"
          @click="nextStep"
        >
          Next →
        </button>
      </div>
    </div>

    <!-- Step 2 -->
    <div v-else-if="step === 2" class="flex flex-col space-y-2">
      <ChatBubble sender="bot">Want to suggest a new brand or product?</ChatBubble>
      <AddBrandForm
        :brandName="newBrandName"
        :productName="newProductName"
        :imageData="newImageData"
        @update:brandName="newBrandName = $event"
        @update:productName="newProductName = $event"
        @update:imageData="newImageData = $event"
      />
      <div class="flex justify-between mt-4">
        <button class="text-gray-600 hover:underline" @click="prevStep">← Back</button>
        <button class="bg-pink-500 hover:bg-pink-600 text-white px-4 py-2 rounded" @click="nextStep">
          Next →
        </button>
      </div>
    </div>

    <!-- Step 3 -->
    <div v-else-if="step === 3" class="flex flex-col space-y-2">
      <ChatBubble sender="bot">How can we reach you?</ChatBubble>
      <ContactForm
        :name="userName"
        :email="userEmail"
        :phone="userPhone"
        @update:name="userName = $event"
        @update:email="userEmail = $event"
        @update:phone="userPhone = $event"
      />
      <div class="flex justify-between mt-4">
        <button class="text-gray-600 hover:underline" @click="prevStep">← Back</button>
        <button
          class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded"
          @click="submitForm"
        >
          Submit →
        </button>
      </div>
    </div>

    <!-- Step 4 -->
    <div v-else class="flex flex-col space-y-2">
      <ChatBubble sender="bot">🎉 Thank you for sharing! Here’s what you submitted:</ChatBubble>
      <div class="bg-gray-100 rounded p-4 space-y-2">
        <p><strong>Name:</strong> {{ userName || 'N/A' }}</p>
        <p><strong>Email:</strong> {{ userEmail || 'N/A' }}</p>
        <p><strong>Phone:</strong> {{ userPhone || 'N/A' }}</p>
        <p><strong>Selected Brands:</strong> {{ selectedBrands.length ? selectedBrands.join(', ') : 'N/A' }}</p>
        <p><strong>Suggested Brand:</strong> {{ newBrandName || 'N/A' }}</p>
        <p><strong>Suggested Product:</strong> {{ newProductName || 'N/A' }}</p>
        <p><strong>Image:</strong> {{ newImageData ? 'Uploaded' : 'N/A' }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import BrandList from './BrandList.vue';
import AddBrandForm from './AddBrandForm.vue';
import ContactForm from './ContactForm.vue';
import ChatBubble from './ChatBubble.vue';

export default {
  components: {
    BrandList,
    AddBrandForm,
    ContactForm,
    ChatBubble
  },
  data() {
    return {
      step: 1,
      selectedBrands: [],
      newBrandName: '',
      newProductName: '',
      newImageData: '',
      userName: '',
      userEmail: '',
      userPhone: ''
    };
  },
  methods: {
    nextStep() {
      if (this.step < 4) this.step++;
    },
    prevStep() {
      if (this.step > 1) this.step--;
    },
    submitForm() {
      this.step = 4;

      // Optional: still send data to Formspree
      fetch("https://formspree.io/f/xleybrdn", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json"
        },
        body: JSON.stringify({
          name: this.userName,
          email: this.userEmail,
          phone: this.userPhone,
          selectedBrands: this.selectedBrands.join(', '),
          suggestedBrand: this.newBrandName || 'N/A',
          suggestedProduct: this.newProductName || 'N/A',
          image: this.newImageData || 'N/A'
        })
      }).catch(() => {});
    }
  }
};
</script>

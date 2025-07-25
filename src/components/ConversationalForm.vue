<template>
  <div class="h-full flex flex-col overflow-hidden text-sm sm:text-base text-gray-800">
    <!-- Step 1 -->
    <div v-if="step === 1" class="h-full flex flex-col">
      <!-- Fixed Chat + Search -->
      <div ref="chatContainerRef" class="shrink-0 bg-[#fcfbf5] px-4 pt-2 pb-1 z-10">
        <div class="flex justify-center">
          <ChatBubble sender="bot">Hey there! 👋 Which skincare brands do you love?</ChatBubble>
        </div>
        <input type="text"
          class="w-full mt-1 px-4 py-2 rounded-full border border-white/30 bg-white/40 backdrop-blur-md shadow-md focus:outline-none focus:ring-2 focus:ring-pink-300 focus:border-transparent placeholder:text-pink-400 text-gray-800 transition duration-200"
          placeholder="🔍 Search skincare brands..." v-model="searchQuery" />
      </div>

      <!-- Scrollable Brand List: grows and scrolls -->
      <div class="flex-1 overflow-y-auto px-4 py-2">
        <div class="flex flex-wrap gap-2 justify-start w-full">
          <div v-for="brand in filteredBrands" :key="brand" @click="toggleBrand(brand)" :class="[
            'cursor-pointer px-4 py-2 rounded-full text-sm transition-all duration-200 border font-medium',
            selectedBrands.includes(brand)
              ? 'bg-pink-500 text-white border-transparent shadow-md scale-105'
              : 'bg-white hover:bg-pink-50 text-gray-700 border-gray-300 hover:shadow-sm'
          ]">
            {{ brand }}
          </div>
        </div>
      </div>

      <!-- Fixed Next Button -->
      <div class="shrink-0 px-4 py-3 bg-white border-t z-20">
        <button @click="goToNextStep" :disabled="selectedBrands.length === 0" class="w-full bg-pink-500 hover:bg-pink-600 text-white font-semibold py-2 px-4 rounded-full shadow-md ring-1 ring-pink-300
         focus:outline-none focus:ring-2 focus:ring-pink-400 transition-all duration-200 transform active:scale-95
         disabled:bg-gray-300 disabled:cursor-not-allowed disabled:ring-0 flex items-center justify-center gap-1">
          Next <span class="text-lg">➡️</span>
        </button>
      </div>
    </div>

    <!-- Step 2 -->
    <div v-else-if="step === 2" class="absolute inset-x-0" :style="{
      top: chatSectionTop + 'px',
      bottom: nextButtonHeight + footerHeight + 'px',
      overflowY: 'auto',
      padding: '0 1rem'
    }">
      <div class="flex justify-center">

        <ChatBubble sender="bot">Want to suggest a new brand or product?</ChatBubble>
      </div>
      <AddBrandForm :brandName="newBrandName" :productName="newProductName" :imageData="newImageData"
        @update:brandName="newBrandName = $event" @update:productName="newProductName = $event"
        @update:imageData="newImageData = $event" />
      <div class="flex justify-between pt-4 pb-8">
        <button @click="prevStep"
          class="flex items-center gap-2 px-4 py-2 rounded-full border border-gray-300 bg-white/50 backdrop-blur-md text-gray-600 hover:bg-white hover:shadow-md hover:text-black transition duration-200">
          <span class="text-lg">←</span>
          <span class="font-medium">Back</span>
        </button>
        <button class="bg-pink-500 hover:bg-pink-600 text-white px-4 py-2 rounded-full shadow-md" @click="nextStep">
          Next →
        </button>
      </div>
    </div>

    <!-- Step 3 -->
    <div v-else-if="step === 3" class="flex flex-col space-y-2">
      <div class="flex justify-center">

        <ChatBubble sender="bot">How can we reach you?</ChatBubble>
      </div>
      <ContactForm :name="userName" :email="userEmail" :phone="userPhone" @update:name="userName = $event"
        @update:email="userEmail = $event" @update:phone="userPhone = $event" />
      <div class="flex justify-between items-center pt-4">
        <!-- Back Button -->
        <button @click="prevStep"
          class="flex items-center gap-2 px-4 py-2 rounded-full border border-gray-300 bg-white/50 backdrop-blur-md text-gray-600 hover:bg-white hover:shadow-md hover:text-black transition duration-200">
          <span class="text-lg">←</span>
          <span class="font-medium">Back</span>
        </button>

        <!-- Submit Button -->
        <button
          class="bg-pink-500 hover:bg-pink-600 text-white px-6 py-2 rounded-full shadow-md transition-all duration-200"
          @click="submitForm">
          Submit →
        </button>
      </div>
    </div>

    <!-- Step 4 -->
    <div v-else class="absolute inset-x-0 px-4 py-6 overflow-y-auto"
      :style="{ top: chatSectionTop + 'px', bottom: footerHeight + 'px' }">
      <ChatBubble sender="bot">🎉 Thank you for sharing! Here's what you submitted:</ChatBubble>

      <div class="bg-white/80 backdrop-blur-md border border-gray-200 rounded-lg p-4 shadow-md space-y-3 mt-3 text-sm">
        <p v-if="submittedData.name"><strong>Name:</strong> {{ submittedData.name }}</p>
        <p v-if="submittedData.email"><strong>Email:</strong> {{ submittedData.email }}</p>
        <p v-if="submittedData.phone"><strong>Phone:</strong> {{ submittedData.phone }}</p>
        <p v-if="submittedData.selectedBrands"><strong>Selected Brands:</strong> {{ submittedData.selectedBrands }}</p>
        <p v-if="submittedData.suggestedBrand"><strong>Suggested Brand:</strong> {{ submittedData.suggestedBrand }}</p>
        <p v-if="submittedData.suggestedProduct"><strong>Suggested Product:</strong> {{ submittedData.suggestedProduct
        }}</p>
        <p v-if="submittedData.image && submittedData.image !== 'N/A'">
          <strong>Image:</strong>
          <a :href="submittedData.image" target="_blank" class="text-blue-600 underline">View uploaded image</a>
        </p>
      </div>

      <!-- Thank you and contact message -->
      <div class="mt-6 text-center text-gray-700 text-sm leading-relaxed px-1">
        <p>Thank you for shaping our collection! 💖</p>
        <p>We're launching in <strong>August</strong>! If you have any questions, feel free to reach out:</p>
        <p class="mt-2">
          📧 <a href="mailto:artisansvale@gmail.com" class="text-pink-600 underline">artisansvale@gmail.com</a><br />
          💬 WhatsApp us: <a href="tel:+15678017023" class="text-pink-600 underline">+1 (567) 801-7023</a><br />
          📸 <a href="https://instagram.com/artisanvale" target="_blank"
            class="text-pink-600 underline">@artisanvale</a>
        </p>
        <p class="mt-2 font-medium">Follow us on Instagram for updates!</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, nextTick } from 'vue';
import ChatBubble from './ChatBubble.vue';
import AddBrandForm from './AddBrandForm.vue';
import ContactForm from './ContactForm.vue';

const step = ref(1);
const searchQuery = ref('');
const selectedBrands = ref([]);
const submittedData = ref({});

const brands = [

  "The Ordinary", "COSRX", "Beauty of Joseon", "Laneige", "Innisfree", "Etude House", "Some By Mi", "Isntree", "Missha", "TONYMOLY", "The Face Shop", "Mamaearth", "Dot & Key", "Minimalist", "Plum Goodness", "Forest Essentials", "mCaffeine", "WOW Skin Science", "The Derma Co.", "Just Herbs", "Biotique",
  "3CE", "A'PIEU", "ABIB", "ABOUT ME", "ACWELL", "AHC", "ALIVE:LAB", "ALL NATURAL", "AMOREPACIFIC", "AMPLE:N", "ANJO", "ANUA", "ANYANG", "AROMATICA", "ATOPALM", "BANILA CO", "BEAUTY OF MAEUM", "BENTON", "BERGAMO", "BEPLAIN", "BEYOND", "BIODERMA", "BIOHEAL BOH", "BLITHE", "BOH", "BRINGGREEN",
  "CENTELLIAN24", "CELIMAX", "CELRANICO", "CENOVIS", "CHICA Y CHICO", "CLAVUU", "CLIO", "COTDE", "CREMORLAB", "CU SKIN", "D'ALBA", "DEAR KLAIRS", "DEWYTREE", "DONGINBI", "DR. CEURACLE", "DR. G", "DR. JART+", "DR. PEPTI", "DR.HEDISON", "DR.JAYS", "DR.ORACLE", "DR.SKINFIX", "E NATURE", "EGF",
  "ELIZAVECCA", "EMUL", "ENPRANI", "EUNYUL", "EVERCOS", "FARMSTAY", "FASCY", "FATION", "FEEV", "FILLIMILLI", "FIRST COSMETIC", "FOODAHOLIC", "FRUDIA", "GENIE IN A BOTTLE", "GILLA8", "GOODAL", "GOODPIE", "GRAYMELIN", "G9SKIN", "HANUR", "HARUHARU WONDER", "HEIMISH", "HERA", "HERBALUX", "HOLIKA HOLIKA",
  "HUXLEY", "I'M FROM", "I'M MEME", "ILLIYOON", "IOPE", "IT'S SKIN", "JAYJUN", "JM SOLUTION", "JOAH", "JUNGSAEMMOOL", "JUMISO", "KAHI", "KILL COVER", "KLAIRS", "KOCOSTAR", "KUMKANG KIND", "LEADERS", "LEBELAGE", "LET ME SKIN", "LIME", "LIMESPA", "LIONHEART", "LOHACELL", "LOVBOD", "LULULUN", "MA:NYO",
  "MAKE P:REM", "MAMONDE", "MEDIHEAL", "MEDIPEEL", "MIZON", "MOONSHOT", "MOTHER MADE", "MR. HONEY", "NACIFIC", "NAMING", "NEOGEN", "NEOGEN DERMALOGY", "NEOZEN", "NINELESS", "NOKDU", "NONGHYUP", "NATURE REPUBLIC", "NUMBUZIN", "OHUI", "ONE THING", "ONSAEMEEIN", "ORJENA", "OSMOPURE", "PACIFICPHARMA",
  "PETITFEE", "PHYSIOGEL", "PIBUBU", "PIBUWANG", "PRO YOU", "PURITO", "PYUNKANG YUL", "REAL BARRIER", "ROUND A’ROUND", "ROUND LAB", "SAMU", "SCINIC", "SECRET KEY", "SELVERT", "SEXYLOOK", "SHANGPREE", "SHANGRI-LA", "SIDMOOL", "SINFUL", "SIXPLUS", "SKIN1004", "SKINFOOD", "SKIN HOUSE", "SKINRx LAB",
  "SNP", "SOMEBYMI", "SOON JUNG", "STAYGANIC", "STAY COOLS", "THANK YOU FARMER", "THE LAB", "THE ORDINARY (KOREA)", "THE PLANT BASE", "THE SAEM", "THE SKIN HOUSE", "THELAVICOS", "TIAM", "TOCOBO", "TORRIDEN", "TOUN28", "TREEANNSEA", "TROIAREUKE", "TRUECARE", "UNPA", "URANG", "VARI:HOPE", "VELY VELY",
  "VT COSMETICS", "WELLAGE", "WISHTREND", "WONJIN EFFECT", "WONDER BATH", "YADAH", "YEHWADAM", "YULIP", "ZEROID", "ZYMOGEN", "9WISHES", "16BRAND", "23 YEARS OLD", "9CC", "BONAJOUR", "CNP LABORATORY", "DERMAFIRM", "ECLADO", "EILEEN GRACE", "GLOW RECIPE (KR)", "K-BEAUTY NATURAL", "LABIOTTE", "MISSDECO",
  "NATUREKIND", "RE:CIPE", "SKIN&LAB", "SKIN79", "SNOWY", "SO NATURAL", "SUR.MEDIC", "WHAMISA"

];

const filteredBrands = computed(() => {
  if (!searchQuery.value) return brands;
  return brands.filter(b =>
    b.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});

function toggleBrand(brand) {
  if (selectedBrands.value.includes(brand)) {
    selectedBrands.value = selectedBrands.value.filter(b => b !== brand);
  } else {
    selectedBrands.value.push(brand);
  }
}

function goToNextStep() {
  step.value += 1;
}
function prevStep() {
  step.value -= 1;
}
function nextStep() {
  step.value += 1;
}
function submitForm() {
  const formData = {
    name: userName.value || '',
    email: userEmail.value || '',
    phone: userPhone.value || '',
    selectedBrands: selectedBrands.value.join(', '),
    suggestedBrand: newBrandName.value || '',
    suggestedProduct: newProductName.value || '',
    image: newImageData.value || ''
  };

  fetch("https://formspree.io/f/mqabwjov", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json"
    },
    body: JSON.stringify(formData)
  })
    .then(async res => {
      if (res.ok) {
        submittedData.value = { ...formData };
        selectedBrands.value = [];
        newBrandName.value = '';
        newProductName.value = '';
        newImageData.value = '';
        userName.value = '';
        userEmail.value = '';
        userPhone.value = '';
        step.value = 4;
      } else {
        const error = await res.json();
        console.error("Formspree Error:", error);
        alert("Oops! Submission failed: " + (error.message || "Unprocessable Content"));
      }
    })
    .catch(err => {
      console.error("Network Error:", err);
      alert("Network error. Please try again later.");
    });
}


// Layout constants
const chatSectionTop = 180; // Same as App.vue pt-[180px]
const nextButtonHeight = 64;
const footerHeight = 72;

// Additional form fields
const newBrandName = ref('');
const newProductName = ref('');
const newImageData = ref(null);
const userName = ref('');
const userEmail = ref('');
const userPhone = ref('');
</script>

<style scoped>
/* Optional: customize scrollbars if needed */
</style>

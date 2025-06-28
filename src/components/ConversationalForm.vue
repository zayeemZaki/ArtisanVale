<template>
  <div class="h-full flex flex-col overflow-hidden text-sm sm:text-base text-gray-800">
    <!-- Step 1 -->
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
    <div v-else-if="step === 2" class="flex flex-col gap-4 px-4">
      <div class="flex justify-center">

        <ChatBubble sender="bot">Want to suggest a new brand or product?</ChatBubble>
      </div>
      <AddBrandForm :brandName="newBrandName" :productName="newProductName" :imageUrl="newImageUrl"
        @update:brandName="newBrandName = $event" @update:productName="newProductName = $event"
        @update:imageUrl="newImageUrl = $event" />

      <div class="flex justify-between items-center pt-4">
        <!-- Back Button -->
        <button @click="prevStep"
          class="flex items-center gap-2 px-4 py-2 rounded-full border border-gray-300 bg-white/50 backdrop-blur-md text-gray-600 hover:bg-white hover:shadow-md hover:text-black transition duration-200">
          <span class="text-lg">←</span>
          <span class="font-medium">Back</span>
        </button>

        <!-- Next Button -->
        <button @click="nextStep"
          class="bg-pink-500 hover:bg-pink-600 text-white px-6 py-2 rounded-full shadow-lg transition-all duration-200">
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

<!-- Step 4: Thank You & Confirmation -->
<div v-else class="flex flex-col h-full overflow-y-auto px-4 pb-32 pt-4 text-center items-center">
  <!-- Thank You Message -->
  <div class="bg-pink-100 text-pink-800 rounded-full px-6 py-2 text-sm mb-6 shadow">
    🎉 Thank you for sharing! Here's what you submitted:
  </div>

  <!-- Summary Card -->
  <div class="bg-white/70 backdrop-blur-md border border-pink-200 p-6 rounded-xl shadow max-w-md w-full text-left text-sm mb-6">
    <p class="mb-2"><strong>Name:</strong> {{ name || 'N/A' }}</p>
    <p class="mb-2"><strong>Email:</strong> {{ email || 'N/A' }}</p>
    <p class="mb-2"><strong>Phone:</strong> {{ phone || 'N/A' }}</p>
    <p class="mb-2"><strong>Selected Brands:</strong> {{ selectedBrands.length ? selectedBrands.join(', ') : 'N/A' }}</p>
    <p class="mb-2"><strong>Suggested Brand:</strong> {{ suggestedBrand || 'N/A' }}</p>
    <p class="mb-2"><strong>Suggested Product:</strong> {{ suggestedProduct || 'N/A' }}</p>
    <p class="mb-0"><strong>Image:</strong> {{ imagePreview ? '✅ Attached' : 'N/A' }}</p>
  </div>

  <!-- Launch Notice -->
  <div class="bg-pink-50 border border-pink-200 rounded-xl p-6 text-sm leading-relaxed max-w-md w-full shadow text-gray-800">
    <p class="mb-2 font-semibold text-pink-700 text-base">
      We're launching in <span class="text-pink-600 font-bold">August 2025!</span> 🛍️
    </p>
    <p class="mb-3">
      Stay tuned — your input helps us shape our perfect skincare lineup. 💖
    </p>
    <p class="mb-1">Have questions? Contact us at:</p>
    <p>
      <a href="mailto:hello@artisanvale.com" class="text-pink-600 underline">hello@artisanvale.com</a> |
      <a href="tel:+11234567890" class="text-pink-600 underline">+1 (123) 456-7890</a>
    </p>
    <p class="mt-3">Follow us on Instagram: 
      <a href="https://instagram.com/artisanvale" target="_blank" class="text-pink-600 underline">@artisanvale</a>
    </p>
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

const brands = [
  "Minimalist", "Dot & Key", "Mamaearth", "WOW Skin Science", "Plum Goodness", "mCaffeine", "The Derma Co.", "Biotique", "Forest Essentials", "Just Herbs",
  "3CE", "A'PIEU", "ABIB", "ABOUT ME", "ACWELL", "AHC", "ALIVE:LAB", "ALL NATURAL",
  "AMOREPACIFIC", "AMPLE:N", "ANJO", "ANUA", "ANYANG", "AROMATICA", "ATOPALM", "BANILA CO",
  "BEAUTY OF JOSEON", "BEAUTY OF MAEUM", "BENTON", "BERGAMO", "BEPLAIN", "BEYOND", "BIODERMA",
  "BIOHEAL BOH", "BLITHE", "BOH", "BRINGGREEN", "CENTELLIAN24", "CELIMAX", "CELRANICO", "CENOVIS",
  "CHICA Y CHICO", "CLAVUU", "CLIO", "COSRX", "COTDE", "CREMORLAB", "CU SKIN", "D'ALBA",
  "DEAR KLAIRS", "DEWYTREE", "DONGINBI", "DR. CEURACLE", "DR. G", "DR. JART+", "DR. PEPTI",
  "DR.HEDISON", "DR.JAYS", "DR.ORACLE", "DR.SKINFIX", "E NATURE", "EGF", "ELIZAVECCA", "EMUL",
  "ENPRANI", "ETUDE HOUSE", "EUNYUL", "EVERCOS", "FARMSTAY", "FASCY", "FATION", "FEEV",
  "FILLIMILLI", "FIRST COSMETIC", "FOODAHOLIC", "FRUDIA", "GENIE IN A BOTTLE", "GILLA8", "GOODAL",
  "GOODPIE", "GRAYMELIN", "G9SKIN", "HANUR", "HARUHARU WONDER", "HEIMISH", "HERA", "HERBALUX",
  "HOLIKA HOLIKA", "HUXLEY", "I'M FROM", "I'M MEME", "ILLIYOON", "INNISFREE", "IOPE", "ISNTREE",
  "IT'S SKIN", "JAYJUN", "JM SOLUTION", "JOAH", "JUNGSAEMMOOL", "JUMISO", "KAHI", "KILL COVER",
  "KLAIRS", "KOCOSTAR", "KUMKANG KIND", "LANEIGE", "LEADERS", "LEBELAGE", "LET ME SKIN",
  "LIME", "LIMESPA", "LIONHEART", "LOHACELL", "LOVBOD", "LULULUN", "MA:NYO", "MAKE P:REM",
  "MAMONDE", "MEDIHEAL", "MEDIPEEL", "MISSHA", "MIZON", "MOONSHOT", "MOTHER MADE", "MR. HONEY",
  "NACIFIC", "NAMING", "NEOGEN", "NEOGEN DERMALOGY", "NEOZEN", "NINELESS", "NOKDU", "NONGHYUP",
  "NATURE REPUBLIC", "NUMBUZIN", "OHUI", "ONE THING", "ONSAEMEEIN", "ORJENA", "OSMOPURE",
  "PACIFICPHARMA", "PETITFEE", "PHYSIOGEL", "PIBUBU", "PIBUWANG", "PRO YOU", "PURITO", "PYUNKANG YUL",
  "REAL BARRIER", "ROUND A’ROUND", "ROUND LAB", "SAMU", "SCINIC", "SECRET KEY", "SELVERT",
  "SEXYLOOK", "SHANGPREE", "SHANGRI-LA", "SIDMOOL", "SINFUL", "SIXPLUS", "SKIN1004", "SKINFOOD",
  "SKIN HOUSE", "SKINRx LAB", "SNP", "SOME BY MI", "SOMEBYMI", "SOON JUNG", "STAYGANIC", "STAY COOLS",
  "THANK YOU FARMER", "THE FACE SHOP", "THE LAB", "THE ORDINARY (KOREA)", "THE PLANT BASE",
  "THE SAEM", "THE SKIN HOUSE", "THELAVICOS", "TIAM", "TOCOBO", "TONYMOLY", "TORRIDEN", "TOUN28",
  "TREEANNSEA", "TROIAREUKE", "TRUECARE", "UNPA", "URANG", "VARI:HOPE", "VELY VELY", "VT COSMETICS",
  "WELLAGE", "WISHTREND", "WONJIN EFFECT", "WONDER BATH", "YADAH", "YEHWADAM", "YULIP", "ZEROID",
  "ZYMOGEN", "9WISHES", "16BRAND", "23 YEARS OLD", "9CC", "BONAJOUR", "CNP LABORATORY", "DERMAFIRM",
  "ECLADO", "EILEEN GRACE", "GLOW RECIPE (KR)", "K-BEAUTY NATURAL", "LABIOTTE", "MISSDECO",
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
  console.log('Form submitted!');
    step.value = 4;

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

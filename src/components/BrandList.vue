<template>
  <div class="flex flex-col h-[calc(100vh-200px)]"> <!-- adjust height based on header+footer -->
    <!-- Search Input (fixed at top of scroll area) -->
    <div class="p-2">
      <input
        type="text"
        class="w-full p-2 border rounded text-sm"
        placeholder="Search brands..."
        v-model="searchQuery"
      />
    </div>

    <!-- Scrollable brand list (takes all available remaining space) -->
    <div class="flex-1 overflow-y-auto px-2 pb-4">
      <div class="flex flex-wrap gap-2">
        <div
          v-for="brand in filteredBrands"
          :key="brand"
          @click="toggleBrand(brand)"
          :class="[
            'cursor-pointer px-3 py-1 rounded-full border text-sm transition',
            selectedBrands.includes(brand)
              ? 'bg-pink-200 text-pink-800 border-pink-400 font-semibold'
              : 'bg-white text-gray-600 border-gray-300 hover:bg-pink-100'
          ]"
        >
          {{ brand }}
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  props: {
    selectedBrands: Array
  },
  data() {
    return {
      brands: [
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
      ],
      searchQuery: ''
    };
  },
  computed: {
    filteredBrands() {
      const query = this.searchQuery.toLowerCase();
      return this.brands.filter(brand => brand.toLowerCase().includes(query));
    }
  },
  methods: {
    toggleBrand(brand) {
      const updated = [...this.selectedBrands];
      const index = updated.indexOf(brand);

      if (index > -1) {
        updated.splice(index, 1);
      } else {
        updated.push(brand);
      }

      this.$emit('update:selectedBrands', updated);
    }
  }
};
</script>

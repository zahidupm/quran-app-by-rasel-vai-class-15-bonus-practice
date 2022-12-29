<template>
  <div class="min-h-screen bg-gray-100">
    <div class="container py-6">
      <div class="bg-white p-4 rounded">
        <div class="flex -mx-4 items-center justify-center">
          <div class="flex-1 px-4 mb-6">
            <select
              @change="getSpecificSurah"
              class="quran-input"
              name=""
              id=""
            >
              <option value="">Select Surah</option>
              <option v-for="sura in suras" :value="sura.number">
                {{ sura.name }} - {{ sura.englishName }}
              </option>
            </select>
          </div>

          <div class="flex-1 px-4 text-center">
            <h3 class="font-bold mb-1 text-lg">Al-Baqrah</h3>
            <p>The Cow</p>
          </div>

          <div class="flex-1 px-4">
            <select class="quran-input" name="" id="">
              <option value="">Select Ayah</option>
            </select>
          </div>
        </div>

        <div class="">
          <p
            class="flex"
            v-if="currentSura.hasOwnProperty('ayahs')"
            v-for="ayah in currentSura.ayahs"
          >
            <span
              class="text-xs mr-2 h-4 w-4 rounded-full flex text-center justify-center border"
              >{{ ayah.numberInSurah }}
            </span>
            -
            {{ ayah.text }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      suras: [],
      currentSura: [],
    };
  },
  mounted() {
    axios.get(`https://api.alquran.cloud/v1/surah`).then((res) => {
      this.suras = res.data.data;
    });
    this.querySpecificSurah(1);
  },
  methods: {
    getSpecificSurah(e) {
      this.querySpecificSurah(e.target.value);
    },
    querySpecificSurah(surahNumber) {
      axios
        .get(`http://api.alquran.cloud/v1/surah/` + surahNumber)
        .then((res) => {
          this.currentSura = res.data.data;
        });
    },
  },
};
</script>

<template>
  <div class="min-h-screen bg-gray-100">
    <div class="container py-6">
      <div class="bg-white p-4 rounded">
        <div class="flex -mx-4 items-center justify-center">
          <div class="flex-1 px-4 mb-6">
            <select class="quran-input" name="" id="">
              <option value="">Select Surah</option>
              <option v-for="sura in suras" value="">
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
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Veniam,
            animi cumque at natus eos hic sunt debitis deleniti consequuntur
            corrupti?
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
    };
  },
  mounted() {
    axios.get(`https://api.alquran.cloud/v1/surah`).then((res) => {
      this.suras = res.data.data;
    });
  },
};
</script>

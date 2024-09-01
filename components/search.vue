<template>
  <form
    class="w-full flex justify-center gap-2.5 my-10 px-2.5"
    @submit.prevent="handleSubmit"
  >
    <input
      type="text"
      placeholder="Search for a coin"
      class="border w-full sm:w-1/2 shadow-sm rounded-md py-2 px-4"
      v-model="search"
    />
    <button
      type="submit"
      class="bg-blue-600 text-white rounded-md py-2 px-4 text-xs sm:text-base"
    >
      Search
    </button>
  </form>
  <Modal
    :isOpen="isOpen"
    :closeModal="closeModal"
    :info="info"
    :loading="loading"
  />
</template>

<script setup>
import axios from "axios";

const config = useRuntimeConfig();
const isOpen = ref(false);
const search = ref("");
const info = ref([]);
const loading = ref(false);

function closeModal() {
  isOpen.value = false;
}
function openModal() {
  isOpen.value = true;
}

const API_KEY = config.public.apiKey;

const getSearch = async (input) => {
  loading.value = true;
  try {
    const url = `https://api.coinranking.com/v2/coins?search=${input}`;

    const options = {
      headers: { "x-access-token": API_KEY },
    };
    const { data } = await axios.get(url, options);
    info.value = data.data.coins[0];
  } catch (error) {
    console.log(error);
  } finally {
    loading.value = false;
  }
};

const handleSubmit = () => {
  if (!search.value.trim()) {
    alert("Input can not be blank");
    closeModal();
  } else {
    getSearch(search.value.trim());
    openModal()
  }
};
</script>

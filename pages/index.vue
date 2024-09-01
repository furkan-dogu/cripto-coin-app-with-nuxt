<template>
    <div class="container mx-auto flex flex-col items-center">
        <h1 class="text-center text-4xl font-bold my-1 tracking-wide pt-5">Crypto Coin App</h1>
        <Search :coins="coins" />
        <Table :coins="coins" />
    </div>
</template>

<script setup>
import axios from 'axios'

const config = useRuntimeConfig();
const coins = ref([])

const API_KEY = config.public.apiKey

const getCoins = async () => {
    const options = {
        headers: { "x-access-token": API_KEY },
    };

    try {
        const { data } = await axios.get("https://api.coinranking.com/v2/coins?limit=100", options)
        coins.value = data.data.coins
    } catch (error) {
        console.log(error);
    }
}

onMounted(() => {
    getCoins()
})

</script>
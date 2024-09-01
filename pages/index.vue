<template>
    <div class="container mx-auto flex flex-col items-center">
        <h1 class="text-center text-4xl font-bold my-1 tracking-wide pt-5">Cyripto Coin App</h1>
        <Search />
        <Table :coins="coins" />
    </div>
</template>

<script setup>
import axios from 'axios'
const coins = ref([])

const API_KEY = process.env.NUXT_API_KEY

const getCoins = async () => {
    const options = {
        headers: { "x-access-token": API_KEY },
    };

    try {
        const { data } = await axios.get("https://api.coinranking.com/v2/coins/", options)
        coins.value = data.data.coins
    } catch (error) {
        console.log(error);
    }
}

onMounted(() => {
    getCoins()
})

</script>
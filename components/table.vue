<template>
    <div class="w-full">
        <table class="w-full text-[9px] sm:text-base">
            <thead>
                <tr class="text-left border-b">
                    <th>Name</th>
                    <th>Rank</th>
                    <th>Symbol</th>
                    <th>Icon</th>
                    <th>Change</th>
                    <th>Price</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="coin in props.coins" :key="coin.uuid" class="border-b font-bold">
                    <td class="text-gray-500">{{ coin.name }}</td>
                    <td :style="{ color: coin.color }">{{ coin.rank }}</td>
                    <td :style="{ color: coin.color }">{{ coin.symbol }}</td>
                    <td>
                        <a :href="coin.coinrankingUrl" target="_blank">
                            <img :src="coin.iconUrl" :alt="coin.name" class="w-4 h-4 sm:w-8 sm:h-8">
                        </a>
                    </td>
                    <td :class='["h-full" ,coin.change < 0 ? "text-red-500" : "text-green-500"]'>
                        <div class="flex items-center justify-start">
                            <span v-if="coin.change < 0"><IconsDown /></span>
                            <span v-else><IconsUp /></span>
                            {{ coin.change }}
                        </div>
                    </td>
                    <td :style="{ color: coin.color }">${{ Number(coin.price).toFixed(2) }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
const props = defineProps(['coins'])
</script>
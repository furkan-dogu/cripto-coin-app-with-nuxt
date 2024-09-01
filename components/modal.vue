<template>
  <TransitionRoot appear :show="isOpen" as="template">
    <Dialog as="div" @close="closeModal" class="relative z-10">
      <TransitionChild
        as="template"
        enter="duration-300 ease-out"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="duration-200 ease-in"
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div class="fixed inset-0 bg-black/25" />
      </TransitionChild>

      <div class="fixed inset-0 overflow-y-auto">
        <div
          class="flex min-h-full items-center justify-center p-4 text-center"
        >
          <TransitionChild
            as="template"
            enter="duration-300 ease-out"
            enter-from="opacity-0 scale-95"
            enter-to="opacity-100 scale-100"
            leave="duration-200 ease-in"
            leave-from="opacity-100 scale-100"
            leave-to="opacity-0 scale-95"
          >
            <DialogPanel
              class="w-full max-w-md transform overflow-hidden rounded-2xl bg-white p-6 text-left align-middle shadow-xl transition-all"
            >
              <div v-if="loading">
                <div class="flex justify-center items-center">
                  <div
                    class="animate-spin rounded-full h-48 w-48 border-b-2 border-gray-900"
                  ></div>
                </div>
              </div>
              <div v-else class="font-anta flex flex-col items-center gap-5 relative">
                <button class="absolute -top-3 -right-3 text-red-600 text-xl" @click="closeModal">
                    <IconsClose />
                </button>
                <div class="flex items-center justify-center">
                    <p class="font-medium text-xl sm:text-3xl text-gray-500 text-center">{{ info.name }}</p>
                    <span class="font-medium text-xs text-white px-2 py-[2px] rounded-full bg-orange-500">{{ info.symbol }}</span>
                </div>
                <p class="font-bold sm:text-2xl text-xl text-gray-800">$ {{ Number(info.price).toFixed(2) }}</p>
                <a :href="info.coinrankingUrl" target="_blank">
                    <img :src="info.iconUrl" :alt="info.name" class="w-24 h-24">
                </a>
                <div :class="['flex justify-center items-center gap-1', info.change < 0 ? 'text-red-500' : 'text-green-500']">
                    <span><IconsChart /></span>
                    <p>{{ info.change }}%</p>
                </div>
                <p class="text-gray-600">RANK:{{ info.rank }}</p>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { ref } from "vue";
import {
  TransitionRoot,
  TransitionChild,
  Dialog,
  DialogPanel,
} from "@headlessui/vue";

const props = defineProps(["isOpen", "closeModal", "info", "loading"]);
</script>

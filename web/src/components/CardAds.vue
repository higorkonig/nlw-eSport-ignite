<script setup lang="ts">
import { computed, ref } from 'vue';

const props = defineProps({
    name: {
        type: String,
        required: true
    },
    yearsPlaying: {
        type: Number,
        required: true
    },
    weekDays: {
        type: Array,
        required: true
    },
    hoursStart: {
        type: String,
        required: true
    },
    hoursEnd: {
        type: String,
        required: true
    },
    useVoiceChannel: {
        type: Boolean,
        required: true
    },
})

const week: string[] = ["Dom", "Seg", "Ter", "Qua", "Qui", "Sex", "Sab"];
const emit = defineEmits(['conecte-player'])


function conectePlayer() {
    emit('conecte-player')
}

const days = computed(() => {
    const dias = props.weekDays.length;
    return `${dias}`;
})

</script>

<template>
    <div class="w-full bg-[#2A2634] py-6 px-9 rounded-md ">
        <div class="text-white mb-2">
            <span class="text-sm text-zinc-400 block">Nome</span>
            <span class="text-sm font-black">{{name}}</span>
        </div>
        <div class="text-white mb-2">
            <span class="text-sm text-zinc-400 block">Tempo de jogo</span>
            <span class="text-sm font-black">{{yearsPlaying}} anos</span>
        </div>
        <div class="text-white mb-2 w-full">
            <span class="text-sm text-zinc-400 block">Disponibilidade</span>
            <span class="text-sm font-black block mt-1">{{days}} dias &#8226; {{hoursStart}} - {{hoursEnd}}</span>
            <span class="text-xs text-zinc-400  font-black" v-for="(day, index) in weekDays"
                :key="index">&nbsp;&#8226;&nbsp;{{week[Number(day)]}}</span>
        </div>

        <div class="text-white mb-2">
            <span class="text-sm text-zinc-400 block">Chamada de áudio?</span>
            <span class="text-sm font-black text-emerald-400" v-if="useVoiceChannel">Sim</span>
            <span class="text-sm font-black text-yellow-500" v-else>Não</span>
        </div>
        <button
            class="bg-violet-500 mt-3 px-4 text-white h-9 rounded-md font-semibold flex items-center gap-3 hover:bg-violet-600 hover:duration-300"
            @click="conectePlayer()">
            <span class="material-symbols-outlined">
                stadia_controller
            </span> Conectar
        </button>
    </div>
</template>
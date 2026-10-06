<script setup>

defineProps({
    title: String,
    body: String,
    id: Number,
    colorText: String
})
const emit = defineEmits([
    'cambiarFavoritoNombre'
])

</script>


<template>
<div class="card">
    <div class="card-body">
        <h5 class="card-title"  :class="`text-${colorText}`">{{ id }}-{{ title }}</h5>
        <p class="card-text">{{ body }}</p>
        <button @click="emit('cambiarFavoritoNombre',title)" class= "btn-primary">Favorito</button>
    </div>

</div>

</template>
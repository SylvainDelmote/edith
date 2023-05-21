<script setup>
const emit = defineEmits(['red', 'yellow', 'green'])
</script>

<template>
<q-bar>
    <div> <!-- IOS Control Btns -->
        <!-- RED -->
        <q-btn @click= "() => emit('red')" dense flat round icon="lens" size="8.5px" color="negative">
            <q-tooltip  class="bg-negative"> Fermer </q-tooltip>
        </q-btn>
         <!-- YELLOW -->
        <q-btn @click= "() => emit('yellow')" dense flat round icon="lens" size="8.5px" color="info">
            <q-tooltip class="bg-warning" > Plein Ecran </q-tooltip>
        </q-btn>

        <!-- GREEN -->
        <q-btn @click= "() => emit('green')"  dense flat round icon="lens" size="8.5px" color="positive">
            <q-tooltip  class="bg-positive text-body-2"> Revenir en haut </q-tooltip>
        </q-btn>
    </div>

    <q-space />

    <q-btn dense flat icon= "sunny" />

    <div style="cursor: pointer;"></div>

    <q-btn dense flat icon="search" />

  </q-bar>
</template>

<script setup>
// IMPORT

// PROPS  & EMITS
const props = defineProps({
  documentIsLocked: {
    type: Boolean
  }
})
const emit = defineEmits(['lockIt', 'addIt', 'saveIt', 'lineIt', 'displayIt'])

// VARIABLES
const couleur = 'primary'

</script>

<template>
  <div  class=" q-gutter-sm dock" style="border-radius: 20px;" >
    <!--AddIt  -->
    <q-btn
      class="dock-btn"
      glossy
      :color=couleur
      icon="add_box"
      :disable= props.documentIsLocked
      @click= "() => emit('addIt')"

      >
      <q-tooltip class="text-body2">Ajouter un bloc Editable</q-tooltip>
    </q-btn>

    <!-- LineIt -->
    <q-btn
      class="dock-btn"
      :color=couleur
      glossy
      icon="add_comment"
      :disable= props.documentIsLocked
      @click= "() => emit('lineIt')"
      >
      <q-tooltip class="text-body2">Rendre la selection editable</q-tooltip>
    </q-btn>

    <!-- BTN - 4 -->
    <q-btn
      class="dock-btn"
      glossy
      :color=couleur
      icon="visibility"
      :disable= props.documentIsLocked
      @click= "() => emit('displayIt')"

      >
      <q-tooltip class="text-body2"> Apercu </q-tooltip>
    </q-btn>

        <!-- SaveIt  -->
        <q-btn
      class="dock-btn"
      glossy
      :color=couleur
      icon="save"
      :disable= props.documentIsLocked
      @click= "() => emit('saveIt')"

      >
      <q-tooltip class="text-body2">Sauvegarder la saisie </q-tooltip>
    </q-btn>

    <!-- LockIt-->
    <q-btn
      class="dock-btn"
      glossy
      :color="props.documentIsLocked ? 'negative' : couleur "
      :icon ="props.documentIsLocked ? 'lock' : 'lock_open' "
      @click= "() => emit('lockIt')"
      >
      <q-tooltip class="text-body2">  {{props.documentIsLocked ? 'Deverrouiller le document' : 'Verrouiller le document'}}</q-tooltip>

    </q-btn>
  </div>
</template>

<style scoped>
.dock{
  min-width: 40vw;
  height: 12vh;
  display: flex;
  justify-content:space-evenly;
  align-items: center;
  backdrop-filter: blur( 20px );
  background-color: rgba(229, 227, 227, 0.848);
  opacity: 0.8;
}

.dock-btn{
  padding: 1rem 1.5rem;
  border-radius: 10px;
  margin: 1rem;
}

.q-btn:hover{
  background: hsl(213, 32%, 52%) !important;

}

@media screen and (max-width: 400px) {
  .dock{
    flex-direction: column;
    min-width: 3rem;
    height: fit-content;
    position: absolute;
    top: -90vw;
    left: 0;
  }
}
@media screen and (max-width: 280px) {
  .dock{
   visibility: hidden;
  }
}

</style>

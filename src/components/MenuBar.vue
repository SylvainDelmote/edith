<script setup>
// IMPORT
import { ref } from 'vue'

// PROPS & EMITS

const MenuIsOpen = ref(false)

</script>

<template>
<q-bar class="bg-dark">

  <q-avatar class="gt-sm" rounded color="primary" size="md" text-color="white" icon="directions" />
  <q-header-title class="gt-sm text-weight-bold"> Edith </q-header-title>

    <!-- Mobile  -->
    <q-btn  flat  class="lt-md" icon="menu" @click="()=> MenuIsOpen = !MenuIsOpen" />
    <div v-if="MenuIsOpen">
            <!-- TODO -->
    </div>

    <!-- Desktop -->

    <q-btn flat no-caps size="14px"   color="white" label="Fichier">
        <q-menu>
          <q-list style="min-width: 100px">
            <q-item clickable v-close-popup>
              <q-item-section>Nouveau document </q-item-section>
            </q-item>
            <q-item clickable v-close-popup>
              <q-item-section> Importer un modele  </q-item-section>
            </q-item>
            <q-separator />
                   <q-item clickable v-close-popup>
              <q-item-section>Sauvegarder comme modele</q-item-section>
            </q-item>

            <q-item clickable v-close-popup>
              <q-item-section>Sauvegarder en local</q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section>Exporter</q-item-section>
            </q-item>
          </q-list>
        </q-menu>
      </q-btn>

    <q-btn flat no-caps size="14px"  color="white" label="Edition">
        <q-menu>
          <q-list style="min-width: 100px">
            <q-item clickable v-close-popup>
              <q-item-section>Copier</q-item-section>
            </q-item>
            <q-item clickable v-close-popup>
              <q-item-section>Coller</q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section>Recents</q-item-section>
            </q-item>
            <q-item clickable v-close-popup>
              <q-item-section>Historique</q-item-section>
            </q-item>

          </q-list>
        </q-menu>
      </q-btn>

    <q-btn flat no-caps size="14px"   color="white" label="Affichage">
        <q-menu>
          <q-list style="min-width: 100px">
            <q-item clickable v-close-popup>
              <q-item-section>New tab</q-item-section>
            </q-item>
            <q-item clickable v-close-popup>
              <q-item-section>New incognito tab</q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section>Recent tabs</q-item-section>
            </q-item>
            <q-item clickable v-close-popup>
              <q-item-section>History</q-item-section>
            </q-item>
            <q-item clickable v-close-popup>
              <q-item-section>Downloads</q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section>Settings</q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section>Help &amp; Feedback</q-item-section>
            </q-item>
          </q-list>
        </q-menu>
      </q-btn>

      <q-btn flat no-caps  size="14px" color="white" label="Fenêtre">
        <q-menu>
          <q-list style="min-width: 100px">
            <q-item clickable v-close-popup>
              <q-item-section>New tab</q-item-section>
            </q-item>
            <q-item clickable v-close-popup>
              <q-item-section>New incognito tab</q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section>Recent tabs</q-item-section>
            </q-item>
            <q-item clickable v-close-popup>
              <q-item-section>History</q-item-section>
            </q-item>
            <q-item clickable v-close-popup>
              <q-item-section>Downloads</q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section>Settings</q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section>Help &amp; Feedback</q-item-section>
            </q-item>
          </q-list>
        </q-menu>
      </q-btn>

        <q-btn flat no-caps size="14px"  color="white" label="Aide">
        <q-menu>
          <q-list style="min-width: 100px">
            <q-item clickable v-close-popup>
              <q-item-section> Aide en Ligne </q-item-section>
            </q-item>
            <q-separator />
            <q-item clickable v-close-popup>
              <q-item-section> Signaler un probleme </q-item-section>
            </q-item>

          </q-list>
        </q-menu>
      </q-btn>

    <q-space />

</q-bar>
</template>

<!-- eslint-disable no-unused-vars -->
<script setup>
//  IMPORT
import MenuBar from 'components/MenuBar.vue'
import TopBar from 'src/components/TopBar.vue'
import EditorDock from 'components/EditorDock.vue'
import { ref, onMounted } from 'vue'
import { useQuasar } from 'quasar'

// VARIABLES
const $q = useQuasar()
const editor = ref('')
const documentIsLocked = ref(false)
const editorRef = ref('')
const redAlertIsActive = ref(false)

// FONCTIONS
function addIt () {
  const edit = editorRef.value
  edit.runCmd('insertHTML', '&nbsp;<div class="editable" > <br>     </div>&nbsp;')
  // edit.runCmd('insertHTML', `&nbsp;<div class="editable" > <br>      <i class="q-icon material-icons cursor-pointer" onclick="this.parentNode.parentNode.removeChild(this.parentNode)">close</i></div>&nbsp;`)
  const el = document.querySelector('.editable')
  el.setAttribute('contenteditable', 'true') // Rend le contenu du span Editable
}

function lineIt () {
  const edit = editorRef.value
  const sel = window.getSelection()
  const selection = sel.toString().trim()
  console.log('selection:', selection, selection.length)
  if (selection.length === 0) {
    addIt()
  } else {
    edit.runCmd('insertHTML', `<span class="editable">${selection} </span>`)
    const el = document.querySelector('.editable')
    el.setAttribute('contenteditable', 'true') // Rend le contenu du span Editable
  }
}

function lockIt () {
  documentIsLocked.value = !documentIsLocked.value
}

function exportIt () {
  const content = editorRef.value.getContentEl()
  navigator.clipboard.writeText(content.innerHTML)
  $q.notify({
    message: 'Contenu copié dans le presse papier',
    color: 'positive',
    textColor: 'white',
    icon: 'content_copy'
  })
}

function newDocument () {
  editor.value = null
}

function saveIt () {
  $q.notify({
    message: 'Sauvegarde faite en locale (en fait non)',
    color: 'positive',
    textColor: 'white',
    icon: 'cloud_done'
  })
  console.log(editorRef.value.getContentEl())
}

function toggleTopScreen () {
  alert('todo')
}

function toggleFullScreen () {
  const target = editor.value
  $q.fullscreen.toggle(target)
}

function toggleRedAlert () {
  redAlertIsActive.value = !redAlertIsActive.value
}

function displayIt () {
  const contenu = editorRef.value.getContentEl()

  const afficherEnA4 = () => {
    const contenuValue = contenu.value
    const aperçuWindow = window.open('', '_blank')
    const aperçuDocument = aperçuWindow.document

    const aperçuHTML = `
    <!DOCTYPE html>
    <html>
      <head>
        <title>Aperçu A4</title>
        <style>
          @page {
            size: A4;
            margin: 0;
          }
          html, body {
            width: 100%;
            height: 100%;
            margin: 0;
            padding: 0;
          }
          .contenu {
            padding: 20px;
          }
        </style>
      </head>
      <body>
        <div class="contenu">${contenuValue}</div>
      </body>
    </html>
  `

    aperçuDocument.open()
    aperçuDocument.write(aperçuHTML)
    aperçuDocument.close()
  }
  afficherEnA4()
}

function onPaste (evt) {
  // Let inputs do their thing, so we don't break pasting of links.
  if (evt.target.nodeName === 'INPUT') return
  let text, onPasteStripFormattingIEPaste
  evt.preventDefault()
  evt.stopPropagation()
  if (evt.originalEvent && evt.originalEvent.clipboardData.getData) {
    text = evt.originalEvent.clipboardData.getData('text/plain')
    editorRef.value.runCmd('insertText', text)
  } else if (evt.clipboardData && evt.clipboardData.getData) {
    text = evt.clipboardData.getData('text/plain')
    editorRef.value.runCmd('insertText', text)
  } else if (window.clipboardData && window.clipboardData.getData) {
    if (!onPasteStripFormattingIEPaste) {
      onPasteStripFormattingIEPaste = true
      editorRef.value.runCmd('ms-pasteTextOnly', text)
    }
    onPasteStripFormattingIEPaste = false
  }
}

// LIFECYCLE
onMounted(() => {

})

</script>

<template>
<q-layout view="hHh lpr lfr">

 <!----- HEADER avec 2 BARRES  ------------>

  <q-header elevated >
    <!----- TOP BARRE TYPE MAC IOS  ------------>
      <TopBar
      @green = "toggleTopScreen"
      @yellow="toggleFullScreen"
      @red ="toggleRedAlert"
      />
  <!-- ---------------------------------------- -->

<!-----  BARRE DE MENU  ------------>
    <MenuBar
    @exportIt = "exportIt"
    @newDoc = "newDocument"
    />
<!-- ---------------------------------------- -->
  </q-header>

<!-------------- EDITOR  ---------------------->
  <q-page-container class="q-ma-xl" >
    <div v-if="!redAlertIsActive" class="q-pa-md q-gutter-sm">
      <q-editor
        v-model="editor"
        ref= "editorRef"
        min-height="70vh"
        :content-style=" {minWidth:'300px',  width: '80vw' }"
        placeholder="Votre prochain projet commence ici"
        @paste="onPaste"
        :readonly= documentIsLocked
        :class="documentIsLocked ? 'bg-main' : 'bg-secondary'"
        :toolbar-rounded =" true"
        :toolbar-push = !documentIsLocked
        :definitions="{

      }"

        :toolbar="[
          ['bold', 'italic', 'strike', 'underline'],
          ['removeFormat'],
          [ 'left','center','right','justify'],
          [ 'undo','redo'],
          [
          {
            label: $q.lang.editor.fontSize,
            icon: $q.iconSet.editor.fontSize,
            fixedLabel: true,
            fixedIcon: true,
            list: 'no-icons',
            options: [
              'size-1',
              'size-2',
              'size-3',
              'size-4',
              'size-5',
              'size-6',
              'size-7'
            ]
          },
          {
            label: $q.lang.editor.defaultFont,
            icon: $q.iconSet.editor.font,
            fixedIcon: true,
            list: 'no-icons',
            options: [
              'default_font',
              'arial',
              'arial_black',
              'comic_sans',
              'courier_new',
              'impact',
              'lucida_grande',
              'times_new_roman',
              'verdana'
            ]
          },

        ],

          ]"
        :fonts="{
          arial: 'Arial',
          arial_black: 'Arial Black',
          comic_sans: 'Comic Sans MS',
          courier_new: 'Courier New',
          impact: 'Impact',
          lucida_grande: 'Lucida Grande',
          times_new_roman: 'Times New Roman',
          verdana: 'Verdana'
      }"

      />
    </div>
    <div v-if="redAlertIsActive">

    </div>
  </q-page-container>
<!-- ---------------------------------------- -->

<!--------- DOCK TYPE IOS ---------------------->
  <q-footer  reveal  class="transparent" >
  <q-toolbar class=" flex flex-center" style="height: 130px;">
    <EditorDock
      @lockIt="lockIt"
      @addIt="addIt"
      @saveIt="saveIt"
      @lineIt = "lineIt"
      @displayIt = "displayIt"
      :documentIsLocked=documentIsLocked
    />
  </q-toolbar>
  </q-footer>
<!-- ---------------------------------------- -->

</q-layout>
</template>

<style>
.transparent{
  background: transparent;
}
</style>

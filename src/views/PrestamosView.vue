

<script lang="ts" setup>
import { ref } from 'vue'
const imgUrl = ref("")
const pasteButton = ref(null)

async function pasteImagen() {
  const r = await navigator.clipboard.readText();
  console.log(r);
}

const pasteImg = async ()=> {
    try {
        const clipboardItems = await navigator.clipboard.read()
        const blobOutput = await clipboardItems[0].getType('image/png')
        if (!blobOutput) {
            console.log('No image found in clipboard')
            return
        }
        const url = URL.createObjectURL(blobOutput)
        
        imgUrl.value = url;
        
    } catch(e) {
        console.log(e);
    }
}

  try {
    // navigator.clipboard.write([
    //     new ClipboardItem({
    //         // 'image/png': pngImageBlob
    //     })
    // ]);
} catch (error) {
    console.error(error);
}
window.onkeydown = function(e) {
    if (e.ctrlKey && e.key == 'v' || e.metaKey && e.key == 'v') {
        console.log("Ctrl + V Pressed !");
        if(!pasteButton.value) return;
        (pasteButton.value as HTMLButtonElement).click();
        // pasteImagen();
    }
};
</script>

<template>
  <div class="about">
    <h1>Esta es la pagina de prestamos</h1>
    <img :src="imgUrl" alt="Logo">

    <button ref="pasteButton" @click="pasteImg()">Pegar imagen</button>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>

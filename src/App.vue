<script setup>
  const archivoUrl = '/Cobblemon%20Chunni%201.3.mrpack'

  function copyToClipboard(text) {

    navigator.clipboard.writeText(document.getElementById(text).value)
  }

</script>

<template>
  <header>
    <div id="h-container">
      <img src="/img/logo.png" alt="Chunnicraft Logo" width="35%"/>
    </div>
  </header>

  <main>
    <div id="m-container">

      <div class="element">
        <label for="ip-address">IP: </label>
        <input type="text" value="mc.chunni.studio" id="ip-address" @click="copyToClipboard('ip-address')" readonly />
        <font-awesome-icon icon="fa-regular fa-copy" class="icon-button" style="cursor:pointer" @click="copyToClipboard('ip-address')" />
      </div>

      <p>Version: 1.21.1</p>
      <p>Plataforma de mods: <a href="https://modrinth.com/" target="_blank" rel="noopener">Modrinth</a></p>
      <p>Modpack Versión 1.3: <a :href="archivoUrl" target="_blank" rel="noopener" style="cursor:pointer">Chunnicraft</a></p>
      <p>Mapa del server: <a href="https://mcmap.chunni.studio/" target="_blank" rel="noopener">Ver Mapa</a></p>

    </div>
  </main>
</template>

<style scoped>

</style>

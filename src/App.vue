<script setup>
  import { ref, onMounted } from 'vue'

  const archivoUrl = '/Cobblemon%20Chunni%201.4.3.mrpack'
  const json = '/mods.json'

  const mods = ref([])

  onMounted(async () => {
    try {
      const response = await fetch(json)
      if (!response.ok) throw new Error('Error al cargar mods.json')
      mods.value = await response.json()
    } catch (error) {
      console.error(error)
    }
  })

  function copyToClipboard(text) {
    navigator.clipboard.writeText(document.getElementById(text).value)
  }

  function trimName(name) {
    return name.replace(/^mods\//, '').replace(/\.jar$/, '').replace(/^datapacks\//, '').replace(/\.zip$/, '').replace(/^resourcepacks\//, '')
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

      <p>Version de Minecraft: 1.21.1</p>
      <p>Plataforma de mods: <a href="https://modrinth.com/" target="_blank" rel="noopener">Modrinth</a></p>
      <p>Modpack Versión 1.4.3: <a :href="archivoUrl" target="_blank" rel="noopener" style="cursor:pointer">Chunnicraft</a></p>
      <p>Mapa del server: <a href="https://mcmap.chunni.studio/" target="_blank" rel="noopener">Ver Mapa</a></p>
    </div>

    <div class="element">
      <h2>Changelog</h2>
      
      <div class="list-container">
        <ul>
          <li>
            <h3>1.4.3 (2025-11-19)</h3>
            <ul>
                <li>: Se añade <a href="https://modrinth.com/datapack/allthemons-x-mega-showdown-legacy">AllTheMons x Mega Showdown v2.9.0</a></li>
                <li>Se actualiza el resto de mods</li>
            </ul>
          </li>
        </ul>
      </div>
    </div>

    <div class="element">
      <h2>Lista de Mods y datapacks</h2>
      <div id="modlist" class="list-container">
        <ul>
          <template v-for="mod in mods">
            <li>
              <a :href="mod.downloads[0]" target="_blank" rel="noopener" style="cursor:pointer">{{ trimName(mod.path) }}</a>
            </li>
          </template>
        </ul>
      </div>
    </div>
  </main>

  <footer>
    <div id="f-container">
      <p>Creado por <a href="https://harpuia.me" target="_blank">Harpuia</a> :)</p>
    </div>
  </footer>
</template>

<style scoped>

</style>

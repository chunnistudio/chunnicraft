<script setup>
  import { ref, onMounted } from 'vue'

  const archivoUrl = '/Cobblemon%20Chunni%201.5.0.mrpack'
  const json = '/mods.json'

const jsonList = ref([])
let mods = ref([])
let datapacks = ref([])
let resourcepacks = ref([])


  onMounted(async () => {
    try {
      const response = await fetch(json)
      if (!response.ok) throw new Error('Error al cargar mods.json')
      jsonList.value = await response.json()
    } catch (error) {
      console.error(error)
    }
    mods.value = jsonList.value.filter(item => item.path.startsWith('mods/'))
    datapacks.value = jsonList.value.filter(item => item.path.startsWith('datapacks/'))
    resourcepacks = jsonList.value.filter(item => item.path.startsWith('resourcepacks/'))
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
      <p>Modpack Versión 1.5.0: <a :href="archivoUrl" target="_blank" rel="noopener" style="cursor:pointer">Chunnicraft</a></p>
      <p>Mapa del server: <a href="https://mcmap.chunni.studio/" target="_blank" rel="noopener">Ver Mapa</a></p>
    </div>

    <div class="element">
      <h2>Changelog</h2>
      
      <div class="list-container">
        <ul>
          <li>
            <h3>1.5.0 (2025-27-12)</h3>
            <ul>
              <li>Se actualiza Cobblemon a la versión 1.7.1 - Pueden revisar lo que trae esta versión <a href="https://wiki.cobblemon.com/index.php/1.7.0" target="_blank">aquí</a></li>
              <li>Se quita el mod: Cobblemon: Ride on! por no ser compatible con Cobblemon 1.7.x</li>
              <li>Se quita el mod: Cobblemon Capture XP por no ser compatible con Cobblemon 1.7.x - Parece estar abandonado</li>
              <li>Se quita el mod: Cobblemon - Dex Rewards por no ser compatible con Cobblemon 1.7.x</li>
              <li>De parte de todo el Staff de Chunni Studio, les deseamos que hayan pasado una feliz navidad y que pasen un feliz año nuevo (●´∀｀●)</li>
            </ul>
          </li>
          <li>
            <h3>1.4.5 (2025-11-22)</h3>
            <ul>
                <li>Se actualiza datapack <a href="https://modrinth.com/datapack/allthemons-x-mega-showdown-legacy" target="_blank">AllTheMons x Mega Showdown v2.9.0</a></li>
                <li>Se actualiza mod <a href="https://modrinth.com/mod/rctmod" target="_blank">Radical Cobblemon Trainers 0.16.11-beta</a></li>
                <li>Se actualiza mod <a href="https://modrinth.com/mod/cobblemon-armors" target="_blank">Cobblemon Armors 1.5.2+1.7.0</a></li>
                <li>Se añade dependencia de Cobblemon: Legendary Monuments <a href="https://modrinth.com/mod/legendary-monuments" target="_blank"></a>Cobblemon: Legendary Monuments 7.2</li>
                <li>Se añade dependencia de Cobblemon: Legendary Monuments <a href="https://modrinth.com/mod/resourceful-lib" target="_blank">Resourceful Lib 3.0.12</a></li>
                <li>Se añade dependencia de Cobblemon: Legendary Monuments <a href="https://modrinth.com/mod/chipped" target="_blank">Chipped 4.0.2</a></li>
            </ul>
          </li> 
          <li>
            <h3>1.4.3 (2025-11-19)</h3>
            <ul>
                <li>Se añade <a href="https://modrinth.com/datapack/allthemons-x-mega-showdown-legacy">AllTheMons x Mega Showdown v2.9.0</a></li>
                <li>Se actualiza el resto de mods</li>
            </ul>
          </li>
        </ul>
      </div>
    </div>

    <div class="element-list">
      
      <div id="modlist" class="list-container list-container2">
        <h2>Lista de Mods</h2>
        <div class="list-block">
          <ul>
          <template v-for="mod in mods">
            <li>  
              <a :href="mod.downloads[0]" target="_blank" rel="noopener" style="cursor:pointer">{{ trimName(mod.path) }}</a>
            </li>
          </template>
        </ul>
        </div>
      </div>

      <div id="datapackslist" class="list-container list-container2">
        <h2>Lista de Datapacks</h2>
        <div class="list-block">
          <ul>
          <template v-for="mod in datapacks">
            <li>  
              <a :href="mod.downloads[0]" target="_blank" rel="noopener" style="cursor:pointer">{{ trimName(mod.path) }}</a>
            </li>
          </template>
        </ul>
        </div>
      </div>

      <div id="resourcepackslist" class="list-container list-container2">
        <h2>Lista de Resourcepacks</h2>
        <div class="list-block">
          <ul>
          <template v-for="mod in resourcepacks">
            <li>  
              <a :href="mod.downloads[0]" target="_blank" rel="noopener" style="cursor:pointer">{{ trimName(mod.path) }}</a>
            </li>
          </template>
        </ul>
        </div>
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

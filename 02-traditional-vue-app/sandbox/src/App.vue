<script>
export default {
  data() {
    return {
      characterList: [],
      favourites: [],
      newCharacter: { name: '', nation: '' }
    }
  },
  methods: {
    addToFavourites(character) {
      this.favourites.push(character)
    },
    addToCharcters() {
      if (this.newCharacter.name && this.newCharacter.nation) {
        this.characterList.push({ ...this.newCharacter })
        this.newCharacter = { name: '', nation: '' }
      } else {
        alert('Please enter name and nation')
      }
    },

    removeFromFavourites(character) {
      this.favourites = this.favourites.filter((fav) => fav.name !== character.name)
    },

    isInFavourites(character) {
      return this.favourites.some((fav) => fav.name === character.name)
    }
  }
}
</script>

<template>
  <div>
    <h1>Characters</h1>
    <p v-if="characterList.length === 0">No characters found.</p>
    <div v-else>
      <h1>Avatar: The Last Airbender</h1>
      <ul>
        <li
          style="display: flex; gap: 1rem"
          v-for="(character, index) in characterList"
          :key="`character.name - ${index}`"
        >
          <span>{{ character.name }} - {{ character.nation }}</span>
          <button v-if="isInFavourites(character)" @click="removeFromFavourites(character)">
            Remove from favourites
          </button>
          <button v-else @click="addToFavourites(character)">Add To favourites</button>
        </li>
      </ul>
    </div>
    <hr />
    <div>
      <h1>Favourites</h1>
      <p v-if="favourites.length === 0">No favourites found.</p>
      <div v-else>
        <ul>
          <li v-for="fav in favourites" :key="`${fav.name}`">{{ fav.name }} - {{ fav.nation }}</li>
        </ul>
      </div>
    </div>
    <hr />
    <h1>Add New characters</h1>
    <div style="display: flex; flex-direction: column; gap: 1rem">
      <div style="display: flex; gap: 1rem; align-items: center">
        <label for="name">Name</label>
        <input type="text" id="name" v-model="newCharacter.name" />
      </div>
      <div style="display: flex; gap: 1rem; align-items: center">
        <label for="name">Nation</label>
        <input
          type="text"
          id="nation"
          v-bind:value="newCharacter.nation"
          v-on:input="newCharacter.nation = $event.target.value"
        />
      </div>
      <button @click="addToCharcters" style="width: 10%">Add character</button>
    </div>
  </div>
</template>

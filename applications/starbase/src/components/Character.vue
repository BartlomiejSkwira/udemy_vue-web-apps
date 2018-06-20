<template>
  <div class='col-md-4' @click='switchCharacter'>
    <div class='character-card'>
      <div class='card-block'>
        <h4 class='card-title'>{{character.name}}</h4>
        <p class='card-text'>
          Height: {{character.height}}
        </p>
        <p class='card-text'>
          Mass: {{character.mass}}
        </p>
        <p class='card-text'>
          id: {{currentId}}
        </p>
        <button class='btn btn-primary' @click.stop='revertCharacter'>Revert character</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['id'],

  data() {
    return {
      character: {},
      previousIds: [],
      currentId: this.id
    }
  },

  methods: {
    fetchCharacter(newId) {
      fetch(`https://swapi.co/api/people/${newId}`, {
        method: 'GET'
      })
        .then(response => response.json())
        .then(json => this.character = json)
    },

    switchCharacter() {
      this.previousIds.push(this.currentId)
      let randomId = Math.floor(Math.random() * 83) + 1
      this.currentId = randomId
      this.fetchCharacter(randomId)
    },

    revertCharacter() {
      let lastId = this.previousIds.slice(-1)[0]
      this.previousIds.splice(this.previousIds.length - 1, 1)
      this.fetchCharacter(lastId)
    }
  },

  created() {
    this.fetchCharacter(this.id)
  }
}
</script>

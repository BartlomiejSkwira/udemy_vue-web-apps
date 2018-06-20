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
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['id'],

  data() {
    return {
      character: {}
    }
  },

  methods: {
    fetchCharacter(id) {
      fetch(`https://swapi.co/api/people/${id}`, {
        method: 'GET'
      })
        .then(response => response.json())
        .then(json => this.character = json)
    },

    switchCharacter() {
      let randomId = Math.floor(Math.random() * 83) + 1
      this.fetchCharacter(randomId)
    }
  },

  created() {
    this.fetchCharacter(this.id)
  }
}
</script>

<template>
  <div>
      <div class="container">
          <input class="text" type="text" v-model="term" @keyup.enter="exe">
          <input class="submit" type="submit"  value="Search" @click="exe">
      </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      term: ''
    }
  },
  methods: {
    async exe () {
      this.$emit('loadStart')
      const { data } = await axios.get(`//itunes.apple.com/search?term=${this.term}&country=jp&entry=musicVideo`)
      this.$emit('loadComplete', {results: data.results})
    }
  }
}

</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  height: 70px;
  padding: 20px;
  background-color: #F85F71;
  box-sizing: border-box;
}

.text {
  width: 50%;
  max-width: 300px;
  padding: .5em;
  border: none;
}

.submit {
  padding: .5em 2em;
  margin-left: 10px;
  color: #fff;
  background-color: #4B9EFA;
  border: none;
  border-radius: 20px;
}
</style>
